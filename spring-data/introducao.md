Para iniciar o projeto entramos no Spring Initializr, aonde será gerado o .zip inicial do projeto após selecionarmos todas as opções do projeto. Salvamos o arquivo em alguma pasta, e importamos na IDE.<br>
Precisamos inicializar o framework para conseguirmos utilizar suas ferramentas dentro da nossa aplicação. Além disso, existem algumas anotações como a @SpringBootApplication que devemos usar. A classe inicial SpringDataApplication.java é a classe responsável por iniciar o Spring.<br>
No arquivo pom.xml, adicionamos a dependência do banco de dados.<br>
No arquivo application.properties, na pasta resources, fazemos a configuração para conexão no banco.
```
spring.datasource.url=jdbc:mysql://localhost:3306/springdata

spring.datasource.username = root
spring.datasource.username = root

spring.datasoruce.testWhileIdle = true
spring.datasource.validationQuery = SELECT 1

spring.datasource.driver-class-name=com.mysql.jdbc.Driver

spring.jpa.show-sql=false
spring.jpa.hibernate.ddl-auto=update
spring.jpa.hibernate.naming-strategy= org.hibernate.cfg.ImproveNamingStrategy       // para o CamelCase do Java
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5InnoDBDialect
```
Depois, conectamos o Dbeaver com o MySQL e criamos o banco de dados com o mesmo nome que colocamos no application.properties.<br>
O Spring Data esconde muitas coisas do JPA, Hibernate, JDBC e dos Drivers. Por isso, algumas coisas ele irá executar por baixo de panos.<br>
Primeiramente criaremos os modelos, dentro do pacote .orm, e dentro desse pacote criaremos as classes modelos que serão as entidades.
```
@Entity
@Table(name = "cargos") // colocamos essa anotação para mostrarmos para o JPA que no banco de dados a tabela se chamará cargos
public class Cargo {

	@Id // anotação que informa que o atributo abaixo será o ID
	@GeneratedValue(strategy = GenerationType.IDENTITY) // definimos que o id será criado automático e qual a estratégia de geração do ID
	private Integer id;
	private String descricao;
}
```
Criamos um pacote chamado repository e criamos uma interface que extenderá CrudRepository. No caso, teríamos um CargoRepository como nome da interface. Essa interface CrudRepository já implementa os métodos básicos com o JPA por baixo.<br>
Para rodarmos algo antes do método main, podemos implementar uma interface chamada CommanLineRunner na classe SpringDataApplication, que possui um método run que roda automaticamente após o método main.<br>
Para utilizarmos o CargoRepository na aplicação precisamos fazer injeção de dependências, pois como ela é uma interface não podemos dar new e utilizar seus métodos.Para injetarmos uma dependência, criamos um construtor da classe SpringDataApplication que recebe o CargoRepository e instancia ele.
```
	public SpringDataApplication(CargoRepository repository) {		// cria uma SpringDataApplication com uma instância do CargoRepository
		this.repository = repository;
	}
```
Para criarmos um registro no banco de dados utilizamos a instancia criada dando um `repository.save`, colocando no método run.
```
	@Override
	public void run(String... args) throws Exception {

		Cargo cargo1 = new Cargo("DESENVOLVEDOR DE SOFTWARE");
		repository.save(cargo1);
		
	}
```
