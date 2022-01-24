- Derived Query: é uma consulta aonde através de um comando Java de um método, o Spring Data pega o método e cria uma Query para o banco de dados sem necessidade de escrevermos código SQL. Para executar uma pesquisa com algo específico, como por exemplo, passado um nome e retornando uma lista de funcionarios, podemos utilizar o método `findBy` adicionando o nome. Esse método nos diz que faremos uma consulta por alguma coisa.
```
	private void buscaFuncionarioNome(Scanner scanner) {
		System.out.println("Nome: ");
		String nome = scanner.next();
		
		List<Funcionario> list = funcionaroRepository.findByNome(nome);
	
		list.forEach(System.out::println);
		
	}
```
Esse método sabe fazer AND, OR, EQUALS, BETWEEN, etc. Todas as funcionalidades de consulta (tipo) estão na documentação. Exemplos:
### Usando Like
Para executar um like (e não um equals, como no exemplo), use:

```
List<Funcionario> findByNomeLike(String nome);
```

O valor do parâmetro nome deve usar o pattern, por exemplo:
```
String nome = "%maria%";
```

### Starting e Ending
Você também pode buscar os funcionários pelo prefixo ou sufixo:

```
List<Funcionario> findByNomeEndingWith(String nome)
```

Ou:

```
List<Funcionario> findByNomeStartingWith(String nome)
```

### Null e not Null
Igualmente podemos pesquisar elemento nulos ou não nulos:

```
List<Funcionario> findByNomeIsNull()
```

Ou não nulos com:

```
List<Funcionario> findByNomeIsNotNull()
```

### Ordenação

```
List<Funcionario> findByNomeOrderByNomeAsc(String nome);
```

### Métodos longos
E como dica, como definimos os critérios de pesquisa por meio do nome do método, precisamos ter cuidado para não criar nomes gigantes e prejudicar a legibilidade. Nesse caso devemos favorecer as consultas com JPQL.
[Documentação]](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods).