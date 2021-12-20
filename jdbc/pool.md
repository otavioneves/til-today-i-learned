O pool de conexões é um intermediário entre o Connection Factory e o JDBC, aonde limitamos a quantidade de conexões simultâneas ao banco de dados, evitando sobrecarga. O pool de conexões é um driver, como o C3P0, que além de fazer funcionar o pool, tem fácil acesso à documentação. Para melhorar essa iteração, utilizamos a interface Datasource para expor todas as conexões do pool para a Connection Factory, sendo que quem informa se tem conexão aberta ou não é o Datasource, respondendo ao Connection Factory.
```
public class ConnectionFactory {

	public DataSource dataSource;

	public ConnectionFactory() {
		// toda vez que o Connection Factory for instanciado, criaremos um pool de conexões.

		ComboPooledDataSource comboPooledDataSource = new ComboPooledDataSource();
		comboPooledDataSource.setJdbcUrl("jdbc:mysql://localhost/loja_virtual?useTimezone=true&serverTimezone=UTC");
		comboPooledDataSource.setUser("root");
		comboPooledDataSource.setPassword("root");

		comboPooledDataSource.setMaxPoolSize(15);

		this.dataSource = comboPooledDataSource;		// a variavel DataSource é o que faz funcionar o pool

	}	

	public Connection recuperarConexao() throws SQLException {
		//		com o pool, não utilizamos mais o Driver Manager.
		//		return DriverManager.getConnection("jdbc:mysql://localhost/loja_virtual?useTimezone=true&serverTimezone=UTC", "root", "root");

		return this.dataSource.getConnection();		// o pool que irá prover a conexão

	}
}
```