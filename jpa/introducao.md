O JPA vem para substituir o JDBC, que tem como desvantagens a alta verbosidade do código e o alto acoplamento com o banco de dados, ou seja, se alterar algum nome de uma tabela no banco de dados precisa alterar também no código Java, nas classes DAO.<br>
Como uma das soluções temos a biblioteca Hibernate, que veio como uma alternativa com o JDBC e o EJB 2.<br>
A especificação padrão do Java é a JPA, que é uma especificação para ORM em Java, fazendo com que a comunicação entre a aplicação e o banco de dados pudesse ser feita em Orientação e Objeto.<br>
Para adicionar o Hibernate no projeto adicionamos uma dependência no pom.xml em um projeto Maven.

```
	<dependencies>
		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-entitymanager</artifactId>
			<version>5.4.27.Final</version>
		</dependency>	
	</dependencies>
```

Além do Hibernate, precisamos colocar a dependência do banco de dados.
```
	<dependency>
    	<groupId>mysql</groupId>
    	<artifactId>mysql-connector-java</artifactId>
    	<version>8.0.26</version>
	</dependency>
```

Além do arquivo pom.xml, precisamos também do persistence.xml, adicionado na pasta META-INF na pasta src/main/resources, aonde adicionamos as tags persistence-unit, com o nome loja e a transaction-type. A tag persistence unit é como se fosse o banco de dados (unidade de persistência), ou seja, precisamos de uma tag para cada banco usado.

```
<?xml version="1.0" encoding="UTF-8"?>
<persistence version="2.2"
    xmlns="http://xmlns.jcp.org/xml/ns/persistence"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_2.xsd">

	<persistence-unit name="loja" transaction-type="RESOURCE_LOCAL">
		<properties>
            <property name="javax.persistence.jdbc.driver" value="com.mysql.jdbc.Driver" />
            <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:8080/loja" />
            <property name="javax.persistence.jdbc.user" value="root" />
            <property name="javax.persistence.jdbc.password" value="root" />
            
			<property name="hibernate.dialect" value="org.hibernate.dialect.MySQL5InnoDBDialect" />
            <property name="hibernate.show_sql" value="true" />
            <property name="hibernate.hbm2ddl.auto" value="create" />
		</properties>	
	</persistence-unit>


</persistence>
```
