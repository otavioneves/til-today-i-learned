### Spring MVC

O Padrão MVC é implementado pelo Spring MVC e tem como característica principal dividir a aplicação em 3 componentes:
- Model: contém as classes de domínio da aplicação, também chamado de modelo. Também possui regras de negócio e a camada de persistência de dados.
- View: contém a interação com o usuário, representa a entrada e a saída de dados.
- Controller: é o componente intermediário que recebe as requisições do usuário vindas do View e interage com o model em busca de resposta a ser retornada ao usuário.

O Spring MVC, através de um recurso abstraído do desenvoledor, chamado Front Controller, que funciona recebendo as requisições do navegador e facilita o trabalho com o protocolo HTTP e a criação de HTML dinamicamente, seguindo boas práticas de desenvolvimento.<br>

Outro recurso que é abstraído pelo Spring é o View (Template), responsável por resolver páginas criadas através dos retornos do Controller.

Podemos iniciar o projeto no Spring Framework através do Spring [Initializr](https://start.spring.io/). Abrimos esse projeto no Eclipse como Maven Project.<br>
Exemplo: para fazer um Hello World, criamos um clase HelloController em um pacote controller. Essa classe irá possui as actions, que irá processar uma requisição do usuário e redirecionar para uma determinada view, no caso um view chamada de hello. A view será um HTML que já vai dentro de uma pasta pré configurada dentro do projeto, a `src/main/resources/templates`.<br>
Após criada a página HTML, hello.html, precisamos avisar o Spring Boot sobre o HelloController, utilizando a anotação `@Controller`. Desse modo, cada método é uma action que o Spring vai mapear as requisições para bater nos método dos nosso controllers.<br>
Para um método ser chamado ele precisa estar mapeado, ou seja, ao chamarmos `localhost:8080/hello`, o método hello precisa ter a anotação `@GetMapping`, que tem como atributo o path que iremos chamar, no caso "/hello".<br>
Para mandar variáveis para a view usamos a HttpServletRequest, e através desse atributo podemos settar os atributos.
```
@Controller
public class HelloController {
	@GetMapping("/hello")
	public String hello(HttpServletRequest request) {
		request.setAttribute("nome", "Mundo");		// (nome do atributo, valor do atributo)
		return "hello";
	}
}
```
```
<html>
	<head>
		<meta charset="UTF-8"/>
	</head>
	<body>
		Oi!	<span th:text="${nome}"></span>
	</body>
</html>
```
Para fazermos qualquer página da aplicação podemos utilizar o mesmo princípio de controller, model e as páginas HTMLs feitas em BootStrap e Thymeleaf.<br>
As classes controller são gerenciadas pelo Spring, então não precisamos criar instâncias das mesmas, assim como uma classe EntityManager do JPA.<br>
Uma classe DTO, Data Transfer Object, é uma classe que serve apenas para transferir objetos. O nome dos atributos da classe tem que ter os mesmos names dos inputs. Utilizamos essas classes DTO pois queremos evitar uma falha de segurança chamada Web Parameter Tampering, que é quando se utilizassemos a classe Pedido diretamente, fosse possível alterar, por manipulação, outros atributos da classe além dos presentes no formulário, evitamos também expor o nosso modelo.<br>
Além disso, qualquer mudança na classe modelo causaria uma mudança no HTML.<br>
Para fazermos redirecionamentos como resultado dos métodos, podemos utilizar o redirect ou o forward. O redirect faz o redirecionamento cliente-side, ou seja, faz uma nova requisição para a URL passada. Já o forward faz o redirecionamento server-side, ou seja, dentro da mesma requisição HTTP. Após fazermos uma requisição POST, sempre usamos redirect.

### Spring Boot
O Spring Boot é um projeto que chegou para facilitar o processo de configuração e publicação de nossas aplicações. A intenção é ter o seu projeto rodando o mais rápido possível e sem complicação, utilizando alguns objetos padrão pré configurados para configuração do projeto.<br>
A configuração padrão é baseada em convenções. Com os módulos reconhecidos o Spring Boot vai reconhecê-los e fornecer uma configuração inicial. Os módulos são disponibilizados no seguinte padrão
- parent: é uma tag para definir qual versão do Spring Boot iremos utilizar.
- dependencies e dependency: é uma tag para definir os módulos à serem utilizados.
- build e plugin: é uma tag, que quando recebe o maven, cria no final um arquivo executável .jar.
Arquivo pom.xml do Mavem:
```
<parent>
	<grupoId>org.springframework.boot</grupoId>
	<artifactId>spring-boot-stater-parent</artifactId>
	<version>1.5.0.RELEASE
</parent>

<dependencies>
	<dependecy>
		<grupoId>org.springframework.boot</grupoId>
		<artifactId>spring-boot-stater-web</artifactId>
	</dependecy>
		<dependecy>
		<grupoId>org.springframework.boot</grupoId>
		<artifactId>spring-boot-stater-jdbc</artifactId>
	</dependecy>
</dependencies>

<build>
	<plugin>
		<plugin>
			<grupoId>org.springframework.boot</grupoId>
			<artifactId>spring-boot-maven-plugin</artifactId
		</plugin>
	</plugin>
</build>
```

### Links Importantes
- Spring-Boot [http://projects.spring.io/spring-boot/]
- Appendix F. Dependency versions [https://docs.spring.io/spring-boot/docs/1.5.10.RELEASE/reference/htmlsingle/#appendix-dependency-versions]
- Spring MVC [https://docs.spring.io/spring-boot/docs/1.5.10.RELEASE/reference/htmlsingle/#howto-spring-mvc]
- Use Thymeleaf 3 [https://docs.spring.io/spring-boot/docs/1.5.10.RELEASE/reference/htmlsingle/#howto-use-thymeleaf-3]
- Appendix A. Common application properties [https://docs.spring.io/spring-boot/docs/1.5.10.RELEASE/reference/htmlsingle/#appendix]