Adicionando ação no html:
- th:action="@{/departamentos/salvar}" = ação que fornece o contexto da aplicação para a url da ação
- th:object="${departamento}" = informa qual variável será responsável em enviar informações para o controller, já como um objeto, e também os dados recebidos serão trazidos por esse variável
- th:field="*{nome}" = nome do atributo a qual o campo estaria vinculado
```
		<div class="container" id="cadastro">
				<form th:action="@{/departamentos/salvar}" th:object="${departamento}" method="POST">
				<div class="form-row">
					<div class="form-group col-md-6">
						<label for="nome">Departamento</label>
						<input type="text"class="form-control" id="nome"
								placeholder="Nome Departamento" autofocus="autofocus" th:field="*{nome}"/>
					</div>
				</div>
				<input type="hidden" id="id" name="id" value="" />
				<button type="submit" class="btn btn-primary btn-sm">Salvar</button>
			</form>
		</div>
```

```
	@PostMapping("/salvar")
	public String salvar(Departamento departamento) {
		departamentoService.salvar(departamento);
		return "redirect:/departamento/cadastrar";
	}
```

Adicionando listagem no html:
- <tr th:each="d : ${departamentos}"> : tag responsável em fazer um for each.
- <td th:text="${d.id}">1</td>: responsável em imprimir dados na tela, utilizando a variável criado no th:each. P valor fixo entre as tags td é automaticamente substituído pelo que será puxado do banco.
```

```

```

```

Colocando condicional para encaminhamento de duas diferentes URLs na mesma tag form.
```
<form  th:action="${departamento.id == null} ? @{/departamentos/salvar} : @{/departamentos/editar}" th:object="${departamento}" method="POST">
```

PAra preencher uma varíavel na URL:
```
<a class="btn btn-info btn-sm" th:href="@{/departamentos/editar/{id} (id=${d.id})}" role="button">
```