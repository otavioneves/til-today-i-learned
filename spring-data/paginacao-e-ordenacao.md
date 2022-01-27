A paginação de consultas é mostrar as consultas em páginas, ao invés de consultar tudo de uma vez. Para fazer a paginação na aplicação utilizando o Spring Data, o nosso repository precisa extender a classe `PagingAndSortingRepository`.
```
@Repository
public interface FuncionarioRepository extends PagingAndSortingRepository<Funcionario, Integer>{
	
}
```
Para implementarmos a paginação utilizamos a Classe PageRequest e Page.
```
	private void visualizar(Scanner scanner) {
		
		System.out.println("Qual pagina voce deseja visualizar? ");
		Integer page = scanner.nextInt();

		PageRequest pageable = PageRequest.of(page, 5, Sort.unsorted()); // (número da página, quantidade de itens por página, e a ordenação
		Page<Funcionario> funcionarios = funcionarioRepository.findAll(pageable); // findAll recebe a pagina que é pra retornar
		
		System.out.println(funcionarios);
		System.out.println("Paginal atual " + funcionarios.getNumber());   // o getNumber retorna em qual página o usuário está
		System.out.println("Elementos totais " + funcionarios.getTotalElements());  // o getTotalElements retorna a quantidade total de elementos
		
		funcionarios.forEach(funcionario -> System.out.println(funcionario.toString()));

	}
```
A ordenação do resultado de uma consulta é feita através do terceiro parâmetros do PageRequest.of. Um dos métodos que podemos colocar em sorte é a Direction, aonde podemos descrever se a ordenação será crescente ou descrescente e o campo que será ordenado.
```
PageRequest pageable = PageRequest.of(page, 5, Sort.Direction.DESC, "nome")
```
Além da PagingAndSortingRepository, existem vários Repositories, utilizados para cada problema específico.<br>