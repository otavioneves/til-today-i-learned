Podemos consultar uma entidade pelo ID ou podemos fazer uma query em uma entidade.<br>
- Para buscar pelo ID, podemos usar o método find.
```
	public Produto buscarPorId(int id) {
		return em.find(Produto.class, id);		// busca a entidade pelo id
	}
```
- Para buscar através de uma query, retornando para uma List na aplicação, podemos usar a linguagem JPQL, que é como se fosse uma linguagem SQL orientada à objetos.
```
	public List<Produto> buscarTodos(){
		String jpql = "SELECT p FROM Produto p";		// o nome na consulta não é da tabela e sim o nome da entidade. Seguido de um alias. Carregue o objeto p (que é a entidade Produto)
		return em.createQuery(jpql, Produto.class).getResultList();		// o método cretadeQuery não faz a consulta, ele apenas prepara. Precisamos do método getResultList para executar a consulta, que nesse caso devolverá um List de Produtos.
	}
```
- Para fazer consultas com filtros utilizamos a mesma consulta em JPQL, agora com o WHERE. Como filtro utilizamos o alias, seguido do ponto e do nome do atributo da entidade, não o nome da coluna, igual ao que iremos pesquisar. Para que ali seja colocado o String que passaremos ao método, colocamos esse :nome e setamos o parâmetro antes de finalizar a consulta, ou seja, antes do .getResultList().

```
	public List<Produto> buscarPorNome(String nome){
		String jpql = "SELECT p FROM Produto p WHERE p.nome = :nome";		// após o where, utilizamos o alias, seguido de ponto e o nome do atributo na classe, não da coluna do banco de dados
		return em.createQuery(jpql, Produto.class).setParameter("nome",nome).getResultList();		// com o método setParameter iremos substituir o nome pelo nome na consulta
	}
```
Podemos também passar o parâmetro por posição e por numeração.
```
	public List<Produto> buscarPorNome(String nome){
		String jpql = "SELECT p FROM Produto p WHERE p.nome = ?1";
		return em.createQuery(jpql, Produto.class).setParameter(1,nome).getResultList();
```

- Para fazer consultas com filtros por uma chave estrangeira, precisamos fazer uma consulta fazendo antes um join por trás do pano, e aí retornando a consulta feita. Ao colocarmos `p.categoria.nome` o JPA já faz o join e busca o atributo nome da tabela categoria.
```
	public List<Produto> buscarPorCategoria(String nome){
		String jpql = "SELECT p FROM Produto p WHERE p.categoria.nome = :nome";		// ao colocarmos p.categoria.nome ele já faz o join e busca o atributo nome da tabela categoria
		return em.createQuery(jpql, Produto.class).setParameter("nome",nome).getResultList();
	}
```

- Para fazer uma consulta de uma parte da entidade, não sendo necessário então puxar a entidade inteira (que seria o que entra após o SELECT e antes do FROM). Ao colocarmos p.preco, o JPA já entende que na query traremos apenas os preços. Utilizamos o método getSingleResult que não retorna um List, como o .getResultList, mas sim um único registro.
```
	public BigDecimal buscarPrecoDoProdutoComNome (String nome){
		String jpql = "SELECT p.preco FROM Produto p WHERE p.nome = :nome";		// ao colocarmos p.preco, o JPA já entende que na query traremos apenas os preços
		return em.createQuery(jpql, BigDecimal.class).setParameter("nome",nome).getSingleResult();		// utilizamos o método getSingleResult que não retorna um List, como o .getResultList, mas sim um único registro.
	}
```