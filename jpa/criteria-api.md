Para fazermos consultas com parâmetros dinâmicos, caso não passarmos nenhum valor no atributo que está na query, deixando assim o parâmetro não obrigatório, mas sim opcional. Manualmente, podemos utilizar if e else para verificar se os parâmetros que estão chegando são nulo ou não. Esse não é o melhor modo de fazer.
```
	public List<Produto> buscarPorParametros(String nome, BigDecimal preco, LocalDate dataCadastro) {
		String jpql = "SELECT p FROM Produto p  WHERE 1=1 "; // gambiarra para deixar o WHERE fixo na consulta, e ir
																// colocando o AND nos if

		if (nome != null && !nome.trim().isEmpty()) {
			jpql = "AND p.nome = :nome ";
		}
		if (preco != null) {
			jpql = "AND p.nome = :nome ";
		}
		if (dataCadastro != null) {
			jpql = "AND p.nome = :nome ";
		}

		TypedQuery<Produto> query = em.createQuery(jpql, Produto.class);

		if (nome != null && !nome.trim().isEmpty()) {
			query.setParameter("nome", nome);
		}
		if (preco != null) {
			query.setParameter("preco", preco);
		}
		if (dataCadastro != null) {
			query.setParameter("dataCadastro", dataCadastro);
		}

		return query.getResultList();
	}
```

A melhor solução é utilizar a Criteria, que é uma outra maneira de realizar consultas, que possui varios métodos para montarmos uma query.
```
	public List<Produto> buscarPorParametrosComCriteria(String nome, BigDecimal preco, LocalDate dataCadastro) {
		
		CriteriaBuilder builder = em.getCriteriaBuilder();
		
		CriteriaQuery<Produto> query = builder.createQuery(Produto.class);
		
		Root<Produto> from = query.from(Produto.class);		// da onde vai disparar o from
		
		Predicate filtros = builder.and();		// objeto que faz os ands, que vai grudando os ands
		
		if (nome != null && !nome.trim().isEmpty()) {
			filtros = builder.and(filtros, builder.equal(from.get("nome"), nome));
		}
		if (preco != null) {
			filtros = 	builder.and(filtros, builder.equal(from.get("preco"), preco));
		}
		if (dataCadastro != null) {
			filtros = 	builder.and(filtros, builder.equal(from.get("dataCadastro"), dataCadastro));
		}
		
		query.where(filtros);
		
		return em.createQuery(query).getResultList();
		
	}
```