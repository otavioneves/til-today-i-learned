Cache é guardar um conteúdo de uma consulta para ser reutilizada em próximas consultas.
```
@Repository
public interface PedidoRepository extends JpaRepository<Pedido, Long>{
	
	
	@Cacheable("books")
	List<Pedido> findByStatus(StatusPedido status, Pageable sort);		// o próprio Spring Data faz o select pra gente, ao colocar o nome certo

	@Query("SELECT p FROM Pedido p JOIN p.user u WHERE u.username = :username")
	List<Pedido> findAllByUsuario(@Param("username") String username);

	@Query("SELECT p FROM Pedido p JOIN p.user u WHERE u.username = :username and p.status = :status")
	List<Pedido> findByStatusAndUser(@Param("username") StatusPedido status, @Param("username") String usernam);
	
}
```
A anotação @EnableCaching habilita o cache na aplicação.
```
@EnableCaching
@SpringBootApplication
public class MudiApplication {

	public static void main(String[] args) {
		SpringApplication.run(MudiApplication.class, args);
	}

}
```