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

- Usando JPQL: para consultas complexas e longos, podemos utilizar o JPQL no lugar dos Derived Queries.
```
	// consulta não está no padrão derivated query, por isso precisamos informar para o Spring Data que isso é uma query, fazemos isso com a anotação @Query, que recebe a consulta em JPQL.
	@Query("SELECT f FROM Funcionario f WHERE f.nome = :nome AND f.salario >= :salario AND f.data = :data")
	List<Funcionario> findNomeSalarioMaiorDataContratacao(String nome,Double salario, LocalDate data);	
```

Em ambos tipos de consulta, temos o problema que se o nome da entidade é composta por duas palavras precisamos mostrar para o Spring Data que precisamos separar.
```
List<Funcionario> findByUnidadeTrabalhos_Descricao(String descricao);
```
OU EM JPQL
```
@Query("SELECT f FROM Funcionario f JOIN f.unidadeTrabalhos u WHERE u.descricao = :descricao")
List<Funcionario> findByUnidadeTrabalhos_Descricao(String descricao);
```


- Native Queries: as consultas nativas são uma consulta com a linguagem do banco de dados.
```
	@Query(value = "SELECT * FROM funcionarios f WHERE f.data >= data", nativeQuery = true)		// o argumento nativeQuery informa que escrevemos a consulta conforme é feito no banco. Se não escrevermos isso ele entender que é um JPQL
	List<Funcionario> findDataContratacaoMaior(LocalDate data);
```

- Derived Queries - queries criadas através de comandos Java
- JPQL - queries criadas através de uma estrutura SQL, porém com os nomes das entidades Java
- Native Query - queries padrões SQL que conseguimos executar no nosso Client SQL