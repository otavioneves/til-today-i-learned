- Para simplificarmos a atribuição de atributos nas classes de modelo, podemos fazer a extração dos atributos para outras classes. Como em Clientes, podemos extrair o nome e o CPF para uma classe chamada Dados Pessoais. Para que a JPA continue mapeando corretamente o nome e CPF na tabela do Cliente, utilizamos a anotação na classe criada chamada @Embeddable, aonde dizemos que essa classe é embutida na Entidade que utilizar ela. Na classe cliente, ao declarar o atributo como classe de DadosPessoais, utilizamos a anotação @Embedded, pedindo para que a JPA embutir os DadosPessoais no mapeamento de Cliente.
```
@Embeddable
public class DadosPessoais {

	private String nome;
	private String cpf;
```
```
	@Embedded
	private DadosPessoais dadosPessoais;
```
Aos métodos que antes utilizavam algo como `getCliente().getNome()` e agora teriam que usar `getCliente().getDadosPessoais().getNome()`, podemos simplesmente criar um método `getNome()` na classe Cliente, que apenas delega para outro método a função de chamar `getDadosPessoais().getNome()`, evitando assim ter que fazer alterações no código inteiro.
```
	public String getNome() {
		return this.dadosPessoais.getNome();
	}
	
	public String getCpf() {
		return this.dadosPessoais.getCpf();
	}
```