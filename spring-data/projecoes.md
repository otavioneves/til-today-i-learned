A feature Projection cria projeções de entidades que possuem os campos de uma consulta específica, mas que na realidade não é uma entidade. Fazemos isso padronizando através de uma interface com os atributos com os nomes do que queremos retornar.
```
	@Query(value = "SELECT f.id, f.nome FROM funcionarios f" , nativeQuery = true)
	List<FuncionarioProjecao> findFuncionariosalario();
```

```
	private void pesquisaFuncionarioSalario() {
		List<FuncionarioProjecao> list = funcionaroRepository.findFuncionarioSalario();
		list.forEach(f -> System.out.println("Funcionario [id:" + f.getId() + " Nome: " + f.getNome() + " Salario: " + f.getSalario()));
	}
```

A interface possuí métodos get dos valores que queremos ter na consulta. O objetivo de criar essa interface é encapsular os valores de retorno da consulta dentro de métodos, criando uma entidade projetada contendo os atributos que queremos apresentar.
```
public interface FuncionarioProjecao {

	Integer getId();
	String getNome();
	Double getSalario();
	
}
```