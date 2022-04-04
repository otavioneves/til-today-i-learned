Podemos utilizar o Spring Security com vários níveis de segurança.<br>
- jdbcAuthentication:

```
@Configuration
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

	@Autowired
	private DataSource dataSource;

	@Override
	protected void configure(HttpSecurity http) throws Exception {
		http
		.authorizeRequests()
			.anyRequest()
			.authenticated()
		.and()
		.formLogin(form -> form
				.loginPage("/login")
				.defaultSuccessUrl("/home", true)
				.permitAll()
		)
		.logout(logout -> logout.logoutUrl("/logout"));
	}

	@Override
	protected void configure(AuthenticationManagerBuilder auth) throws Exception {

		BCryptPasswordEncoder encoder = new BCryptPasswordEncoder();
		
		auth.jdbcAuthentication().dataSource(dataSource).passwordEncoder(encoder);

	}
}
```

Criando um usuário

```
		UserDetails user = User.builder().username("carol").password(encoder.encode("carol")).roles("ADM").build();

		auth.jdbcAuthentication().dataSource(dataSource).passwordEncoder(encoder).withUser(user);
```