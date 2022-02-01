Para validação utilizamos o Java Bean Validation através de anotations que aplicamos diretamente no atributo na classe modelo, de modo que apliquemos alguma validação.
```
	@NotBlank
	private String nomeProduto;
	@NotBlank
	private String urlProduto;
	@NotBlank
	private String urlImagem;
```
Aplicamos a anotação @Valid no método que utilizará os atributos para integrar o pedido de execução da validação.
```
	@PostMapping("novo")
	public String novo(@Valid RequisicaoNovoPedido requisicao, BindingResult result) {
		
		if (result.hasErrors()) {
			return "pedido/formulario";
		}
		
		Pedido pedido = requisicao.toPedido();	// convertendo um requisição em um pedido
		pedidoRepository.save(pedido);			
		
		return "pedido/formulario";
	}
```

Com o Thymeleaf podemos integrar alertas de erros e salvamento de preenchimentos ao dar erro em um preenchimento.

```
			<form th:object="${requisicaoNovoPedido}" class="card-body" action="/pedido/novo" method="POST">
				<div class="form-group">
					<label for="nomeProduto">Produto</label>
					<input th:field="*{nomeProduto}"class="form-control" placeholder="Nome do Produto" />
					<small>Informe o nome do produto.</small>
				</div>
```

Para mostrar quais os erros de um preenchimento após uma validação podemos utilizar o th:erros
```
					<div th:errors="*{nomeProduto}">
						Erros do nome do produto
					</div>
```