O Spring Security é um projeto Spring responsável pela segurança das aplicações. Para adicioná-lo no projeto podemos subir no pom.xml a dependência.
```
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>5.6.1</version>
</dependency>
```
Criamos uma classe no pacote principal, que extende WebSecurityConfigurerAdapter. Temos temos que colocar as anotações @Configuration e @EnableWebSecurity. Criamos em seguida um método configuree para configurar o como e onde será feita a autentição e o método userDetailService para configurar usuário e senha. Essa implementação não deve ser utilizada em produção, apenas em fase inicial de testes ou exemplos.
```
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;

@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http.authorizeRequests().anyRequest().authenticated().and().httpBasic();
	}

	@Bean
	@Override
	public UserDetailsService userDetailsService() {
		UserDetails user = User.withDefaultPasswordEncoder().username("otavio").password("otavio").roles("ADM").build();

		return new InMemoryUserDetailsManager(user);
	}

}
```
Essa é a configuração mais básica.
Podemos também criar uma página de login, para isso, podemos usar a configuração que define qual a página responsável pelo login.
```
	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http.authorizeRequests().anyRequest().authenticated().and().formLogin(form -> form.loginPage("/login").permitAll());
	}
```
```
<html>
<head th:replace="~{base :: head}"></head>
<body>

	<div th:replace="~{base :: logo}"></div>

	<div class="container">

		<div th:replace="~{base :: titulo('Login')}"></div>


		<div class="card mb-3">
			<form th:action="@{/login}" method="post">
				<div class="form-group">
					<label for="username">Usuário</label>
					<input name="username" class="form-control" placeholder="Usuário"/>
				</div>
				<div class="form-group">
					<label for="password">Senha</label>
					<input type="password" name="username" class="form-control" placeholder="Senha"/>
				</div>
				
			</form>
		</div>
	</div>
</body>
</html>
```
O Spring Security vai cuidar do método POST para /login, ou seja, fazendo uma requisição POST com usuário e login para /login ele resolve. O GET para mostrar a página precisamos configurar, para isso fazemos um LoginController.
```
@Controller
public class LoginController {

	@GetMapping
	@RequestMapping("/login")
	public String login() {
		return "/login";
	}
}

```
Toda a configuração do Spring Security ficou centralizada em uma única classe e alguns recursos foram usados para que esta configuração funcionasse. A primeira é as suas dependências: nada compilaria se não tivéssemos adicionados a dependência do módulo de segurança no pom.xml: spring-boot-starter-security.<br>
Com isso, nos foi disponibilizado todas as classes necessárias para configurar o módulo de segurança: utilizamos um adapter (WebSecurityConfigurerAdapter), que vem com várias configurações default. Apenas duas destas configurações nós precisamos reimplementar: configure(HttpSecurity) e configure(AuthenticationManagerBuilder auth). Utilizamos uma anotação (@EnableWebSecurity) que disponibiliza todas as dependências do Spring Security que precisamos para configurá-lo conforme a necessidade do nosso projeto; além disso, ganhamos alguns builders, que nos permitiu criar usuários e configurar a autorização.<br>
Para utilizarmos no HTML informações se o usuário já estiver logado mostrar algo e se não estiver mostrar outra, podemos usar um recurso do Thymeleaf com o Spring, adicionanado a dependência a abaixo e escrevendo o código também conforme abaixo.
```
		<dependency>
			<groupId>org.thymeleaf.extras</groupId>
			<artifactId>thymeleaf-extras-springsecurity5</artifactId>
		</dependency>
```

```
<div th:fragment="logo"
	class="logo-container margin mb-3 p-3 d-flex justify-content-between">
	<span class="logo">mudi</span> <span class="mt-3">
	<a class="text-light" sec:authorize="!isAuthenticated()" href="/login">Login</a>
	<a class="text-light" sec:authorize="isAuthenticated()" href="/logout">Logout</a>
	</span>
</div>
```
No WebSecurityConfig temos que determinar o logout no método configure.