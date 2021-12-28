- Consultas usando função de agregação, como sum, min, max, avg, etc. Utilizamos também o JPQL.
```
	public BigDecimal valorTotalVendido() {
		String jpql = "SELECT SUM(p.valorTotal) FROM Pedido p";
		return em.createQuery(jpql, BigDecimal.class).getSingleResult();
	}
```
Caso passemos uma função que o banco de dados não conheça, ele vai lançar uma Exception. Ao usar uma função nativa, devemos ter esse cuidado.

- Consultas para relatórios. Como em consultar para relatórios temos diversas informações de diversas tabelas, uma de cada tipo, podemos usar os comandos SQL no JPQL para unir tabelas, como JOIN, GROUP BY, ORDER BY. Utilizamos também o select new, que cria uma instância de uma classe dentro de uma query, utilizado para quando uma classe não é uma entidade.
```
	public List<RelatorioDeVendaVO> relatorioDeVendas(){
		String jpql = "SELECT new br.com.otavio.loja.vo.RelatorioDeVendaVO( "		// select new cria uma instância da classe que não é uma entidade. Da um new passando as informações para o construtor
				+ "produto.nome, "
				+ "SUM(item.quantidade), "
				+ "MAX(pedido.data)) FROM "
				+ "Pedido pedido "
				+ "JOIN pedido.itens item "
				+ "JOIN item.produto produto "
				+ "GROUP BY produto.nome "
				+ "ORDER BY item.quantidade DESC";
		return em.createQuery(jpql, RelatorioDeVendaVO.class).getResultList();
	
	}
```

- Consultas com named queries. É uma extração de uma consulta da classe DAO para a classe da entidade. Para isso utilizamos a anotação @NameQuery que recebe os parâmetros name, com o nome da query, e o parâmetro query, que é a própria query.