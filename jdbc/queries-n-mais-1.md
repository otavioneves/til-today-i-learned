Devemos ter cuidado ao fazer um programa que faz consulta ao banco de dados, pois podemos fazer uma query pra trazer alguma informação. No código abaixo, por exemplo, temos n queries para trazer os produtos separados por categoria. Quando temos muitos dados no banco, isso pode causar um problema, pois fazemos uma consulta pra trazer cada grupo de dados.
```
	public static void main(String[] args) throws SQLException {

		try(Connection connection = new ConnectionFactory().recuperarConexao()){

			CategoriaDAO categoriaDAO = new CategoriaDAO(connection);

			List<Categoria> listaDeCategorias = categoriaDAO.listar();

			listaDeCategorias.stream().forEach(ct -> {

				System.out.println(ct.getNome());

				try {
					for (Produto produto : new ProdutoDAO(connection).buscar(ct)) {
						System.out.println(ct.getNome() + " - " + produto.getNome());
					}
				} catch (SQLException e) {
					e.printStackTrace();
				}
			});
		}
	}
```
```
public class CategoriaDAO {

	private Connection connection;

	public CategoriaDAO(Connection connection) {
		this.connection = connection;
	}
	
	public List<Categoria> listar() throws SQLException{
		List<Categoria> categorias = new ArrayList<>();
		
		System.out.println("Executando a Query de listar categoria");
		
		String sql = "SELECT ID, NOME FROM CATEGORIA";
		
		try(PreparedStatement pstm = connection.prepareStatement(sql)){
			pstm.execute();
			
			try(ResultSet rst = pstm.getResultSet()){
				
				while (rst.next()) {
					Categoria categoria = new Categoria(rst.getInt(1),rst.getString(2));
					
					categorias.add(categoria);
				}
			}
			
		}
		
		return categorias;
		
	}
}
```
```
	public List<Produto> buscar(Categoria ct) throws SQLException {

		List<Produto> produtos = new ArrayList<Produto>();

		System.out.println("Executando a Query de buscar produto por categoria");
		
		String sql = "SELECT ID, NOME, DESCRICAO FROM PRODUTO WHERE CATEGORIA_ID = ?";
		
		try (PreparedStatement pstm = con.prepareStatement(sql)){	
			
			pstm.setInt(1, ct.getId());
			pstm.execute();

			try (ResultSet rst = pstm.getResultSet()) {
				while (rst.next()) {
					Produto produto = new Produto(rst.getInt(1), rst.getString(2), rst.getString(3));

					produtos.add(produto);
				}
			}
		}

		return produtos;
	}
```
Para evitar consultas de n+1, podemos utilizar o inner join. Dessa maneira, fazemos apenas uma consulta ao banco de dados, trazendo todas as informações.
```
public class TestaListagemDeCategorias {

	public static void main(String[] args) throws SQLException {

		try(Connection connection = new ConnectionFactory().recuperarConexao()){

			CategoriaDAO categoriaDAO = new CategoriaDAO(connection);

			List<Categoria> listaDeCategorias = categoriaDAO.listarComProdutos();

			listaDeCategorias.stream().forEach(ct -> {

				System.out.println(ct.getNome());

				for (Produto produto :ct.getProdutos()) {
					System.out.println(ct.getNome() + " - " + produto.getNome());
				}
			});
			
		}
	}
```
```
	public List<Categoria> listarComProdutos() throws SQLException {

		Categoria ultima = null;

		List<Categoria> categorias = new ArrayList<>();

		System.out.println("Executando a Query de listar categoria");

		String sql = "SELECT C.ID, C.NOME, P.ID, P.NOME, P.DESCRICAO, P.CATEGORIA_ID FROM CATEGORIA C INNER JOIN PRODUTO P ON C.ID = P.CATEGORIA_ID";

		try(PreparedStatement pstm = connection.prepareStatement(sql)){
			pstm.execute();

			try(ResultSet rst = pstm.getResultSet()){

				while (rst.next()) {

					if (ultima == null || !ultima.getNome().equals(rst.getString(2))) {
						Categoria categoria = new Categoria(rst.getInt(1),rst.getString(2));

						ultima = categoria;

						categorias.add(categoria);

					}
					
					Produto produto = new Produto(rst.getInt(3), rst.getString(4), rst.getString(5));
					ultima.adicionar(produto);
					
				}
			}
		}

		return categorias;
	}
```