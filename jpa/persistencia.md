Para persistir um registro de um produto no banco de dados, no JPA existe uma interface chamada EntityManager, que faz a gestão das entidades. Essa interface é responsável por fazer qualquer operação no banco de dados. Para criar um EntityManager utilizamos o EntityManagerFactory, assim como o Connection. A factory vai chamar a Classe Persistence com o método `createEntityManagerFactory("")`, que recebe com parâmetro o nome do persistence-unit, que é a unidade de persistência, ou seja, o banco de dados.<br>
Após criado a Factory, podemos criar um EntityManager.

```
		EntityManagerFactory factory = Persistence.createEntityManagerFactory("loja");
		
		EntityManager em = factory.createEntityManager();
```

- Para adicionar um registro no banco utilizamos o comando ``. Como o que vamos adicionar é um objeto de uma classe de uma entidade, o JPA já entende qual tabela do banco de dados ele irá incluir.

```
		em.persist(celular);
```
