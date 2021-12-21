Toda tabela no banco de dados é mapeada para uma entidade, que nada mais é que uma classe java, para que assim a JPA entenda nosso banco. Adicionamos a classe no src/main/java, e ela representará uma entidade (uma linha) do banco de dados.

- No MySQL:
```
CREATE TABLE produtos (
ID INT AUTO_INCREMENT,
NOME VARCHAR(50) NOT NULL,
DESCRICAO VARCHAR(250) NOT NULL,
PRECO DECIMAL NOT NULL,
PRIMARY KEY(ID))
```

- Na classe Java A anotação @Entity informa que essa classe é uma entidade. A anotação @Table informamos através de name qual o nome da tabela no banco de dados. Os nomes das colunas do banco se tornam varíaveis na classe, esse processo se chama mapeamento. Para informar qual é a chave primária utilizamos a anotação @Id:

```
package br.com.otavio.loja.modelo;

import java.math.BigDecimal;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name= "produtos")
public class Produto {
	
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private int id;
	private String nome;
	private String descricao;
	private BigDecimal preco;
	

}
```

Além de adicionar as entidades como classes, precisamos passar dentro do arquivo persistence.xml, na tag persistence-unit, com a tag class o caminho completo da classe. O Hibernate mapeia isso automaticamente, porém, ao colocar uma entidade, precisamos colocar todas.
```
<class>br.com.otavio.loja.modelo.Produto</class>
```