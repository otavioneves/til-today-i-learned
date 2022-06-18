Para validação utilizamos o Java Bean Validation através de anotations que aplicamos diretamente no atributo na classe modelo, de modo que apliquemos alguma validação.
```
	@NotBlank
	private String nomeProduto;
	@NotBlank
	private String urlProduto;
	@NotBlank
	private String urlImagem;
```
Existes outras validações, como para verificar que o número mínio 5 e no máximo 20 de caracteres. As anotações estão presentes na [documentação](https://docs.jboss.org/hibernate/beanvalidation/spec/2.0/api/javax/validation/constraints/package-summary.html)
```
public class RequisicaoNovoPedido {

    @NotBlank @Min(5) @Max(20)
    private String nomeProduto; 

}
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
<form th:object="${requisicaoNovoPedido}" class="card-body" action="/pedido/novo" method="POST">
	<div class="form-group">
		<label for="nomeProduto">Produto</label>
		<input th:field="*{nomeProduto}"class="form-control is-invalid" placeholder="Nome do Produto" />
		<small>Informe o nome do produto.</small>
		<div class="invalid-feedback" th:errors="*{nomeProduto}">
			Erros do nome do produto
		</div>
	</div>
```
Para alterar a mensagem de erro podemos manipular a anotação @NotBlank, definindo nossas mensagens em um arquivo messages.properties, salvo no resources.
```
NotBlank.requisicaoNovoPedido.nomeProduto=Campo obrigatório
NotBlank.requisicaoNovoPedido.urlProduto=Campo obrigatório
NotBlank.requisicaoNovoPedido.urlImagem=Campo obrigatório
```


Outro modo é utilizando anotações na classe de Domínio.
- @NotBlank(message="O nome do cargo é obrigatório."): obrigatoriedade em não deixar branco.
- @Size(max=60, message = "O nome do cargo deve conter no máximo {max} caracteres."): obrigatoriedade no tamanho do item.

Após marcar os atributos com essas anotações, vamos na classe Controller respectiva e adicionamos nos atributos dos métodos que fazem alterações nos campos, a anotação @Valid na frente do atributo à ser validade, e o atributo BindingResult para verificação de houve algum erro nas validações.

```
@PostMapping("/salvar")
	public String salvar(@Valid Departamento departamento, BindingResult result, RedirectAttributes attr) {
		
		if(result.hasErrors()) {
			return "/cargo/cadastro";
		}
		
		departamentoService.salvar(departamento);
		attr.addFlashAttribute("success", "Departamento inserido com sucesso.");
		return "redirect:/departamentos/cadastrar";
	}
```

No HTML, podemos criar um fragment e chamar nos formulários.