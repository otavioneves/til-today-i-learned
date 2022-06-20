Um modo de fazer validação é utilizando anotações na classe de Domínio.
- @NotBlank(message="O nome do cargo é obrigatório."): obrigatoriedade em não deixar branco.
- @Size(max=60, message = "O nome do cargo deve conter no máximo {max} caracteres."): obrigatoriedade no tamanho do item.
- @NotNul
- Entre outras;

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

No HTML, podemos criar um fragment e chamar nos formulários.<br>

Outra maneira de criar as mensagens de validação é utilizando um arquivo ValidationMessages.properties no Class Path da aplicação, padronizando assim as mensagens de retorno de validação. Essas padronizações podem ser feitas diretamente na anotação ou criando uma chave que é adicionado no atributo .message da validação.

```
javax.validation.constraints.NotNull.message= É obrigatório.

NotNull.funcionario.cargo= Selecione um cargo.
```

Dessa maneira, são três formas de validação. Uma utilizando as anotações de validação definindo o atributo message no seu campo. Outra utilizando as message padronizadas para cada anotação de validação (padronização feita no ValidationMessages.properties). Outra criando uma chave específica para uma anotação em determinado atributo de determinada classe, sobrecarregando a padronização anterior.
<br>
Para criar validações mais complexas é utilizar o Spring Validator, com isso, teremos validações mais específicas atendendo a casos específicos. Para isso, criamos um pacote Validator, no pacote Web, que implementar a classe Validator. Essa classe possuí um método que verificará se os objetos à serem validados são do tipo correto e outro método que faz a validação.

```
public class FuncionarioValidator implements Validator{

	@Override
	public boolean supports(Class<?> clazz) {		// valida o objeto que está sendo enviado do formulário com a classe a ser validada
		return Funcionario.class.equals(clazz);
	}

	@Override
	public void validate(Object object, Errors errors) {		// após passar pelo teste do suporte, faz a validação nesse método
		
		Funcionario f = (Funcionario) object;
	
		LocalDate entrada = f.getDataEntrada();		// data que foi colocada no formulário
		
		if (f.getDataSaida() != null) {		// como data de saída pode ser nulo, validaremos esse campo apenas se não for nulo
			if (f.getDataSaida().isBefore(entrada)) {
				errors.rejectValue("dataSaida", "PosteriorDataEntrada.funcionario.dataSaida");
			}
		}
	}
}
```

Nesse caso, criamos a mensagem de validação no arquivo messages.properties (nome próprio da especificação BeanValidation), com a mensagem da chave PosteriorDataEntrada.funcionario.dataSaida.

```
PosteriorDataEntrada.funcionario.dataSaida = Data de saída deve ser posterior a data de entrada.
```

Para que a validação seja atividada, temos que criar um método que ficará no começo do controller, para que o Spring inicie a validação já no começo.

```
	@InitBinder
	public void initBinder(WebDataBinder binder) {
		binder.addValidators(new FuncionarioValidator());
	}
```



Para validação utilizamos o Java Bean Validation através de anotations que aplicamos diretamente no atributo na classe modelo, de modo que apliquemos alguma validação.

```
	@NotBlank
	private String nomeProduto;
	@NotBlank
	private String urlProduto;
	@NotBlank
	private String urlImagem;
```

Existem outras validações, como para verificar que o número mínimo 5 e no máximo 20 de caracteres. As anotações estão presentes na [documentação](https://docs.jboss.org/hibernate/beanvalidation/spec/2.0/api/javax/validation/constraints/package-summary.html)

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