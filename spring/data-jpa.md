Utilizando um ORM, como o Hibernate, é possível fazer de maneira mais ágil o mapeamento de entidade e registros no banco de dados. O Spring Data JPA já trabalha com o Hibernate.<br>
Uma das formas de organizar é criar uma classe abstrata com alguns métodos comuns entre as classes de persistência. Esse classe se chama AbstractEntity.<br>
Além disso, segundo as boas práticas, sempre que trabalharmos com framework ORM, as classes implementarão Serializable.
```
package com.otavio.curso.demo.domain;

import java.io.Serializable;
import java.util.Objects;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.MappedSuperclass;

@SuppressWarnings("serial")
@MappedSuperclass		// informa para a JPA que esse será uma superclasse para as outras classes.
public abstract class AbstractEntity<ID extends Serializable> implements Serializable {		// implementa já a Serializable, levando isso para todas as classes filhas dessa classe AbstractEntity

	// ao definir que a classe é abstrata, as classes filhas que quiserem utilizar essa classe só poderão utilizá-la como herança, e não por instância
	
	@Id @GeneratedValue(strategy = GenerationType.IDENTITY)		//anotação para marcar que esse atributo abaixo é um ID. A segunda anotação é para gerenciar a estratégia de geração automática desse ID
	private ID id;

	public ID getId() {
		return id;
	}

	public void setId(ID id) {
		this.id = id;
	}

	@Override
	public int hashCode() {
		return Objects.hash(id);
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		AbstractEntity<?> other = (AbstractEntity) obj;
		return Objects.equals(id, other.id);
	}

	@Override
	public String toString() {
		return "id=" + id;
	}
	
}
```

Além disso, precisamos configurar o arquivo application.properties.
```
spring.datasource.url=jdbc:mysql://localhost:3306/demo?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=root
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.open-in-view = true
spring.jpa.hibernate.naming-strategy=org.hibernate.cfg.ImproveNamingStrategy
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasoruce.testWhileIdle=true
spring.datasource.validationQuery=SELECT 1
```

Para a camada de persistência, criamos uma classe no pacote DAO, chamado AbstractDao. Essa clase dará a base para as outras classes DAO.
```
package com.otavio.curso.demo.dao;

import java.io.Serializable;
import java.lang.reflect.ParameterizedType;
import java.util.List;

import javax.persistence.EntityManager;
import javax.persistence.PersistenceContext;
import javax.persistence.TypedQuery;

public abstract class AbstractDao<T, PK extends Serializable> {

	@SuppressWarnings("unchecked")
	private final Class<T> entityClass = (Class<T>) ((ParameterizedType) getClass().getGenericSuperclass())
			.getActualTypeArguments()[0];

	@PersistenceContext
	private EntityManager entityManager;

	protected EntityManager getEntityManager() {
		return entityManager;
	}

	public void save(T entity) {

		entityManager.persist(entity);
	}

	public void update(T entity) {

		entityManager.merge(entity);
	}

	public void delete(PK id) {

		entityManager.remove(entityManager.getReference(entityClass, id));
	}

	public T findById(PK id) {

		return entityManager.find(entityClass, id);
	}

	public List<T> findAll() {

		return entityManager.createQuery("from " + entityClass.getSimpleName(), entityClass).getResultList();
	}

	protected List<T> createQuery(String jpql, Object... params) {
		TypedQuery<T> query = entityManager.createQuery(jpql, entityClass);
		for (int i = 0; i < params.length; i++) {
			query.setParameter(i + 1, params[i]);
		}
		return query.getResultList();
	}

}

```

Após isso criamos uma classe DaoImpl, que implementará uma classe Dao.

```

```

A melhor prática para gerenciar transações é utilizar na camada de serviço, com a anotação @Transactional. Essa anotação recebe o atributo readOnly, que ao ser definido como true, informa que o método não faz nenhuma transação no banco de ados, e apenas lê. Quando uma transação é aberta no banco de dados, a tabela fica travada, já na leitura não. Os métodos de consulta recebe o atributo readOnly = true. O sistema de transações fica na camada service pois o rollback da camada dao não faz o rollback total de um método, no caso de algum erro. Na camada service, caso alguma parte do método tenha algum problema, ele da rollback no método inteiro, evitando pontas soltas.