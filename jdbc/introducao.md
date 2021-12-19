O JDBC (Java Database Connectivity) é uma camada de abstração Java que faz a conexão entre uma aplicação Java e um Banco de Dados. Essa abstração se tornou a biblioteca `java.sql`. Nessa biblioteca nós temos a interface chamada Connection, que tem o DriveManager que recuperará a conexão com o banco de dados, através de dados passados, como tipo de banco de dados, usuário, senha, database, etc.<br>
Para fazer uma primeira conexão com o banco de dados, adicionar no build path uma lib do MySQL Connector, para conexão com o MySQL. Após isso, podemos abrir e fechar a conexão.
```
	public static void main(String[] args) throws SQLException {

		Connection connection = DriverManager.getConnection("jdbc:mysql://localhost/loja_virtual?useTimezone=true&serverTimezone=UTC", "root", "root");
	
		connection.close();
	}
```
### AÇÕES BÁSICAS UTILIZANDO STATEMENT (mais à frente será aprimorada para PreparedStatement)
Para fazer um comando SQL utilizamos o Statement, através do método createStatement() que retorna um objeto Statement. Através desse objeto podemos chamar o método execute, que retorna um booleano, que é true se o retorno do comando for uma lista, e false se for algo que não retornada nada como um DELETE.<br>
Para pegar os dados dessa lista podemos utilizar o comando `.getResultSet`, que retorna um objeto ResultSet. O ResultSet aliado ao método next podemos criar um laço com o while para verificar se existem próximos produtos, se existir, executamos o loop trazendo os resultados.

```
	public static void main(String[] args) throws SQLException {
		
		Connection con = DriverManager.getConnection("jdbc:mysql://localhost/loja_virtual?useTimezone=true&serverTimezone=UTC", "root", "root");
	
		Statement stm = con.createStatement();
		boolean resultado = stm.execute("SELECT ID, NOME, DESCRICAO FROM PRODUTO");
	
		System.out.println(resultado);
		
		ResultSet rst = stm.getResultSet();
		
		while (rst.next()) {
			Integer id = rst.getInt("ID");		// podemos trazer da label ou pelo index (1,2,3,4...)
			System.out.println(id);
			
			String nome = rst.getString("NOME");
			System.out.println(nome);
			
			String descricao = rst.getString("DESCRICAO");
			System.out.println(descricao);			
		}
		
		con.close();
	}
```

Podemos utilizar o padrão FactoryMethods, para criar um Classe que irá criar uma instância de um objeto, fazendo uma fabrica de conexão, aonde sempre que precisarmos de uma conexão com o banco de dados, chamamos esse método. Esse padrão é interessante pois criamos objetos sem expor a lógica ou as configurações de criação ao cliente. Além disso, podemos nos referir ao objeto recém-criado usando uma interface (usando uma abstração), desacoplando a implementação.
```
public class ConnectionFactory {
	public Connection recuperarConexao() throws SQLException {
		return DriverManager.getConnection("jdbc:mysql://localhost/loja_virtual?useTimezone=true&serverTimezone=UTC", "root", "root");
	}
}

```

Para fazermos inserção de dados no banco, abrimos também a conexão e chamamos o comando através do Statement. Podemos utilizar o método do Statement para retorna a PK gerada do valor inserido.

```
	public static void main(String[] args) throws SQLException {

		ConnectionFactory criaConexao = new ConnectionFactory();
		Connection con = criaConexao.recuperarConexao();	
		
		Statement stm = con.createStatement();
		stm.execute("INSERT INTO PRODUTO (nome,descricao) VALUES ('Mouse','Mouse sem fio')",Statement.RETURN_GENERATED_KEYS);
		
		ResultSet rst = stm.getGeneratedKeys();
		
		while(rst.next()) {
			Integer id = rst.getInt(1);		// passamos como parâmetro a coluna 1, que é a primeira coluna
			
			System.out.println("O id criado foi: " + id);
		}
						
		con.close();
		
	}
```

Para deletarmos dados da tabela seguimos a mesma lógica.

```
	public static void main(String[] args) throws SQLException {

		ConnectionFactory criaConexao = new ConnectionFactory();
		Connection con = criaConexao.recuperarConexao();	
		
		Statement stm = con.createStatement();
		stm.execute("DELETE FROM PRODUTO WHERE ID>2");
		
		Integer linhasmodificadas = stm.getUpdateCount();		// o método retorna um inteiro, que é quantas linhas foram modificadas na tabela
		
		System.out.println("Quantidade de linhas modificadas: " + linhasmodificadas);	
		con.close();
		
	}
```

Podemos fazer esses métodos de outra maneira, por exemplo, para inserção, podemos utilizar parâmetros. Porém, temos que ter cuidados com as SQLs Injections, se colocarmos uma concatenação no formulário digitado pelo usuário no comando. Para resolver isso podemos ao invés de criar o statement, preparar o statement, e o JDBC vai controlar a criação. Passamos então os parâmetros com ? na linha de comando do MySQL.

```
		PreparedStatement stm = con.prepareStatement("INSERT INTO PRODUTO (nome,descricao) VALUES ?,?",Statement.RETURN_GENERATED_KEYS);
		stm.setString(1, nome);
		stm.setString(2, descricao);
		
		stm.execute();		// como a query já está preparada podemos apenas executar o Statement
			
	}
```

Com isso, o que digitarmos na variavel nome e descricao será colocado através do set, e não como uma String. Todas as 