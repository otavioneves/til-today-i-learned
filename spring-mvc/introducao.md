O Spring MVC facilita o trabalho com o protocolo HTTP e a criação de HTML dinamicamente, seguindo boas práticas de desenvolvimento.<br>
Uma aplicação MVC em Java utilizando o Spring pode utilizar:
- o Spring Boot no lado do servidor, que utiliza o Tomcat internamente. O Spring Boot gerencia o sistema;
- o Spring MVC no lugar do Servlet, que já possui um Servlet pré configurado;
- O Controller tem a responsabilidade de tratar a requisição. É colocado antes do modelo, após o Spring MVC. Ele possui os métodos que vai no modelo para buscar o que a requisição está requisitando, e devolver para o Spring MVC;
- No lugar do JSP, podemos utilizar o Thymeleaf, junto com o Bootstrap e uma SpringEL.<br>
Podemos iniciar o projeto no Spring Framework através do Spring [Initializr](https://start.spring.io/). Abrimos esse projeto no Eclipse como Maven Project.<br>
Exemplo: para fazer um Hello World, criamos um clase HelloController em um pacote controller. Essa classe irá possui as actions, que irá processar uma requisição do usuário e redirecionar para uma determinada view, no caso um view chamada de hello. A view será um HTML que já vai dentro de uma pasta pré configurada dentro do projeto, a `src/main/resources/templates`.<br>
Após criada a página HTML, hello.html, precisamos avisar o Spring Boot sobre o HelloController, utilizando a anotação `@Controller`. Desse modo, cada método é uma action que o Spring vai mapear as requisições para bater nos método dos nosso controllers.<br>
Para um método ser chamado ele precisa estar mapeado, ou seja, ao chamarmos `localhost:8080/hello`, o método hello precisa ter a anotação `@GetMapping`, que tem como atributo o path que iremos chamar, no caso "/hello".<br>
Para mandar variáveis para a view usamos a HttpServletRequest, e através desse atributo podemos settar os atributos.
```
@Controller
public class HelloController {
	@GetMapping("/hello")
	public String hello(HttpServletRequest request) {
		request.setAttribute("nome", "Mundo");		// (nome do atributo, valor do atributo)
		return "hello";
	}
}
```
```
<html>
	<head>
		<meta charset="UTF-8"/>
	</head>
	<body>
		Oi!	<span th:text="${nome}"></span>
	</body>
</html>
```
Para fazermos qualquer página da aplicação podemos utilizar o mesmo princípio de controller, model e as páginas HTMLs feitas em BootStrap e Thymeleaf.<br>
As classes controller são gerenciadas pelo Spring, então não precisamos criar instâncias das mesmas, assim como uma classe EntityManager do JPA.<br>
Uma classe DTO, Data Transfer Object, é uma classe que serve apenas para transferir objetos. O nome dos atributos da classe tem que ter os mesmos names dos inputs. Utilizamos essas classes DTO pois queremos evitar uma falha de segurança chamada Web Parameter Tampering, que é quando se utilizassemos a classe Pedido diretamente, fosse possível alterar, por manipulação, outros atributos da classe além dos presentes no formulário, evitamos também expor o nosso modelo.<br>
Além disso, qualquer mudança na classe modelo causaria uma mudança no HTML.