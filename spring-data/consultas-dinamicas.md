Para fazer consultas dinâmicas no Spring Data, semelhante ao que é feito na Criteria API, só que de maneira mais enxuta e performática. Para isso, podemos utilizar a implementação no repository chamado `JpaSpecificationExecutor`. Essa implementação é uma interface que abstrai todos os conceitos da Criteria API.
```
@Repository
public interface FuncionarioRepository extends PagingAndSortingRepository<Funcionario, Integer>, JpaSpecificationExecutor<Funcionario >{		// <Nome da Classe, Tipo do Id>
	
}
```
Para criarmos a especificação criamos classes em um pacote chamado Specification, aonde colocamos os métodos para realizar a consulta dinâmica. O objetivo da Specification é entregar, ao desenvolver um objeto pronto, para que ele só tenha que se preocupar com qual operação SQL ele deseja executar.
```
package br.com.otavio.spring.data.specification;

public class SpecificationFuncionario {

	public static Specification<Funcionario> nome(String nome) {	// o nome do método é o atributo que queremos consultar na base de forma dinâmica
		
		return (root, criteriaQuery, criteriaBuilder) -> criteriaBuilder.like(root.get("nome"), "%" + nome + "%");
		//	a Specificaion já possui os atributos root, criteriaQuery e criteriaBuilder, podendo assim útilizamos diretamente, sem implementar.
		
		
	}
	
}
```

Criamos então um service que implementará essa classe. 

```
	public void inicial(Scanner scanner) {
		
		System.out.print("Digite o nome: ");
		String nome = scanner.next();
		
		List<Funcionario> funcionarios = funcionarioRepository.findAll(Specification.where(SpecificationFuncionario.nome(nome)));
		
	}
```

Para outras specification, a base estrutural é a semelhante.
```
public class SpecificationFuncionario {

	public static Specification<Funcionario> nome(String nome) {	// o nome do método é o atributo que queremos consultar na base de forma dinâmica
		return (root, criteriaQuery, criteriaBuilder) -> criteriaBuilder.like(root.get("nome"), "%" + nome + "%");
		//	a Specificaion já possui os atributos root, criteriaQuery e criteriaBuilder, podendo assim útilizamos diretamente, sem implementar.
	}
	
	public static Specification<Funcionario> cpf(String cpf) {
		return (root, criteriaQuery, criteriaBuilder) -> criteriaBuilder.equal(root.get("cpf"), "%" + cpf + "%");		// tipo de busca equal
	}
	
	public static Specification<Funcionario> salario(Double salario) {
		return (root, criteriaQuery, criteriaBuilder) -> criteriaBuilder.greaterThan(root.get("salario"), "%" + salario + "%");		// tipo de busca GreaterThan
	}
	
	public static Specification<Funcionario> dataContratacao(LocalDate dataContratacao) {
		return (root, criteriaQuery, criteriaBuilder) -> criteriaBuilder.greaterThan(root.get("dataContratacao"), "%" + dataContratacao + "%");
	}
	
}
```