Podemos fazer um modelo da tabela no Java, para que as varíaveis na aplicação Java não sejam definidas dentro do código, mas encapsuladas em uma classe separada, chamada modelo. Além de fazer o modelo, podemos fazer uma classe de Persistência, que ela sim irá trabalhar com as informações do Produto no Banco de dados. Essa classe é chamada de Data Acess Object, ou DAO.<br>
Esse pacote DAO recebe as classes que irão tratar tudo que é referente ao acesso ao banco de dados para trabalhar com as informações, como alteração, inclusão, exclusão, tendo cada um seu método. O DAO é um pattern da linguagem onde tudo que é de acesso a objetos, como no banco de dados, possuí o sufixo DAO.<br>

```
public class ProdutoDAO {

	private Connection con;

	public ProdutoDAO(Connection connection) {
		this.con = connection;
	}

	public void salvar(Produto produto) throws SQLException {

		String sql = "INSERT INTO PRODUTO (NOME, DESCRICAO) VALUES (?,?)";

		try (PreparedStatement pstm = con.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS)){

			pstm.setString(1, produto.getNome());
			pstm.setString(2, produto.getDescricao());

			pstm.execute();

			try (ResultSet rst = pstm.getGeneratedKeys()) {
				while (rst.next()) {
					produto.setId(rst.getInt(1));
				}
			}
		}

	}

}
```
```
	public static void main(String[] args) throws SQLException {

		Produto comoda = new Produto("Cômoda","Cômoda Vertical");

		try (Connection con = new ConnectionFactory().recuperarConexao()){
			
			ProdutoDAO produtoDao = new ProdutoDAO(con);
			
			produtoDao.salvar(comoda);
			
		}

	}
```

Com essa abordagem, podemos fazer com que na classe DAO tenhamos todos os métodos que manipulam os dados no banco, como por exemplo, adicionar o método de listagem dos produtos. Podemos na nossa aplicação apenas instanciar a classe DAO e chamar os métodos como preferirmos.
```
	public List<Produto> listar() throws SQLException {

		List<Produto> produtos = new ArrayList<Produto>();

		String sql = "SELECT ID, NOME, DESCRICAO FROM PRODUTO";

		try (PreparedStatement pstm = con.prepareStatement(sql)){	
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

```
	public static void main(String[] args) throws SQLException {

		Produto comoda = new Produto("Cômoda","Cômoda Vertical");

		try (Connection con = new ConnectionFactory().recuperarConexao()){

			ProdutoDAO produtoDao = new ProdutoDAO(con);

			produtoDao.salvar(comoda);

			List<Produto> listaDeProdutos = produtoDao.listar();
			listaDeProdutos.stream().forEach(lp -> System.out.println(lp));

		}
	}
```