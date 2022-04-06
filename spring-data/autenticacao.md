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

Associar acessos no sistema à um usuário (pedimos para o parâmetro principal que retorna o usuário logado, para inserirmos no find)

```
@Repository
public interface PedidoRepository extends JpaRepository<Pedido, Long>{

	@Query("SELECT p FROM Pedido p JOIN p.user u WHERE u.username = :username")
	List<Pedido> findAllByUsuario(@Param("username") String username);
	
}
```

```
	@GetMapping
	public String home(Model model, Principal principal) {
		List<Pedido> pedidos = pedidoRepository.findAllByUsuario(principal.getName());
		model.addAttribute("pedidos",pedidos);
		return "home";
	}
```

Criando novos registros relacionados ao usuário logado (usamos a classe SecurityContextHolder)
```
@Controller
@RequestMapping("pedido") // todas as requisições que forem pra pedido cai nesse controller
public class PedidoController {
	
	@Autowired
	private PedidoRepository pedidoRepository;	// classe que faz o relacionamento com o banco de dados

	@Autowired
	private UserRepository userRepository;

	
	@PostMapping("novo")
	public String novo(@Valid RequisicaoNovoPedido requisicao, BindingResult result) {
		
		if (result.hasErrors()) {
			return "pedido/formulario";
		}
		
		String username = SecurityContextHolder.getContext().getAuthentication().getName();
		User user = userRepository.findByUsername(username);
		
		Pedido pedido = requisicao.toPedido();	// convertendo um requisição em um pedido
		pedido.setUser(user);
		pedidoRepository.save(pedido);			
		
		return "redirect:/home";
	}
}
```

```
@Repository
public interface UserRepository extends JpaRepository<User, String>{

	User findByUsername(String username);
	
}
```
Contexto configurável automaticamente no HTML
```
<form th:action="@{/pedido/novo}
```