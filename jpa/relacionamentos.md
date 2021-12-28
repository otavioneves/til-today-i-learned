- Para relacionamentos muitos para muitos, onde muitas colunas se relacionam e precisam formar uma nova tabela, ao invés de utilizar a anotação @ManyToMany que a JPA já vai entender que é pra fazer um join entre tabelas, nós criamos uma nova entidade com os dados dessa nova tabela que queremos.
```
@Entity
@Table(name = "itens_pedido")
public class ItemPedido {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private int id;
	private BigDecimal precoUnitario;
	private int quantidade;
	@ManyToOne
	private Pedido pedido;
	@ManyToOne
	private Produto produto;
```

- Para relacionamentos bidirecionais, aonde temos mapeados relacionamentos de uma classe para outra e dessa outra classe para essa uma, precisamos informar isso para a JPA, porque se não ela vai fazer um join para cada relacionamento, e não juntar os dois e fazer uma tabela só. Utilizamos na anotação que não irá gerar uma nova tabela o argumento `(mappedBy = "relacioanemto que irá gerar a tabela correta"`, geralmente colocado no lado do OneToMany.
```
	@OneToMany(mappedBy = "pedido")
	private List<ItemPedido> itens = new ArrayList<>();
```

- Quando dentro de um relacionamento muitos para muitos, ao settar em um lado precisamos já settar em outro.
```
	public void adicionarItem(ItemPedido item) {
		item.setPedido(this);		// o item conhece o pedido
		this.itens.add(item);		// o pedido conhece os itens
	}
```

- Além do argumento mappedBy podemos passar o argumento `cascade`, que irá informar que tudo que for feito com o Pedido será feito com o ItemPedido também.
```
	@OneToMany(mappedBy = "pedido",cascade = CascadeType.ALL)
	private List<ItemPedido> itens = new ArrayList<>();
```