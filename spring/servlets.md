Os Servlet são objetos que podemos chamar através do protocolo HTTP, que gera uma resposta html, porém não é estático, já que o Servlet deixa a resposta dinâmica.<br>
Para criarmos um servlet, criamos uma classe que extende a classe HttpServlet. Ela irá sobreescrever o método service.<br>
Para darmos um nome a pagina que será chamada nesse método, utilizamos a anotação `@WebServlet(urlPatterns = /nomedesejado)`.<br>
No mundo HTTP podemos devolver dois tipos de resposta, podendo ser um fluxo binário (como o OutputStream) ou devolver uma página HTML (através do Writer).<br>
```
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;


@WebServlet(urlPatterns = "/oi")
public class OlaMundoServlets extends HttpServlet {

	@Override
	protected void service(HttpServletRequest req, HttpServletResponse resp) throws IOException {
 
		PrintWriter out = resp.getWriter();
		out.println("<html>");
		out.println("<body>");
		out.println("Olá Mundo!");
		out.println("</body>");
		out.println("</html>");

	}

}

```
Para acessar uma página do Tomcat utilizamos protocolo://ip:porta/contexto/recurso. No caso da classe, utilizamos o nome colocado na anotação da Classe.<br>
Através da URL é possível enviar parâmetros para o servidor, utilizando o `?`.
```
http://localhost:8080/gerenciador/novaEmpresa?nome=Alura
```
No lado do servidor, podemos ler o parâmetro com o `getParameter`. Esse método sempre retorna uma string e recebe como parâmetro o nome do parâmetro recebido na requisição.
```
		String nomeEmpresa = request.getParameter("nome");
```
Outra forma de enviar um parâmetro é através do método POST e GET. Dependendo da aplicação, não queremos enviar os dados pelo GET, e sim pelo POST. O método POST precisa receber um formulario, um arquivo .html que irá receber os parâmetros. Um formulário pelo `form`, por padrão usa o método GET, por isso precisamos deixar claro que queremos usar o método POST.
```
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	
	<form action="/gerenciador/novaEmpresa" method = "post">
	
		Nome: <input type="text" name="nome" />
	
		<input type = "Submit" />
	
	</form>
	
</body>
</html>
```
Para deixarmos claro que o método só poderá receber post utilizamos o método `doPost`, caso queira apenas o GET utilizamos o método `doGet`.<br>
As funcionalidades que irão tratar os dados recebidos são colocados no modelo da aplicação. O modelo ou domínio são as classes que representam o mundo real, aquilo que o cliente ou usuário da aplicação define. Para descobrir quais são as classes e funcionalidades do modelo analisamos cada funcionalidade.<br>

Para não escrevermos HTML no código java, utilizamos o JSP, que é uma página HTML que podemos colocar código Java. Para isso utilizamos os marcadores `<% %>`, onde o código java vai dentro deles.
```
<%
	String nomeEmpresa = "Alura";
	System.out.println(nomeEmpresa);
%>

<html>
<body>
	Empresa <% out.println(nomeEmpresa); %> Cadastrada com sucesso!
</body>
</html>
```
No lado do Servlet, precisamos chamar o JSP que possuí o código HTML. Para isso, usamos o método `getRequestDispatcher`, do lado do request, que recebe o nome do endereço do jsp. Chamamos o jsp pelo dispachador.
```
// no código

RequestDispatcher rd = request.getRequestDispatcher("/novaEmpresaCriada.jsp");
rd.forward(request, response);
```
Para jogar algo do código java para o JSP, utilizamos o request do método forward utilizado acima. Para isso penduramos antes na requisição através do `setAttribute` no request.
```
// no código

request.setAttribute("empresa", empresa.getNome());
```
```
// no JSP
String nomeEmpresa = <String> request.getAttribute("empresa");
System.out.println(nomeEmpresa);
```
Os Scriplets dentro do código HTML, assim como código HTML dentro do Java, não são boas práticas. Algumas melhores práticas são: <br>
- Para imprimirmos uma varíavel no código podemos utilizamos expressões, que tem a seguinte sintaxe: `${ }`.
```
<html>
	<body>
		Empresa ${empresa} Cadastrada com sucesso!
	</body>
</html>
```
Podemos também usar uma lib externa de JSP, a JSP JSTL Core, onde fazemos a importação e colocamos o prefixo "c". Para executar o laço, utilizamos a tag `<forEach` dessa lib, que vem antes de definir o laço, utilizando os items e uma expressão. A Lib Core é utilizada para controle de fluxo e para o trabalho de URL.
```
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ page import = "java.util.List, br.com.otavio.gerenciador.servlet.Empresa"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Java Standar Taglib</title>
</head>
<body>

	<ul>
		<c:forEach items="${empresas}" var="empresa">
				<li>${empresa.nome} </li>
		</c:forEach>
	</ul>

</body>
</html>
```
Uma tag que podemos usar dessa biblioteca é a `<url>`, que precede o atributo `value`, deixando assim uma parte do endereço dinâmico. Dentrodessa expressão é substituído o valor do projeto, como o gerenciador.
```
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<c:url value="/novaEmpresa" var ="linkServletNovaEmpresa"/>

<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	
	<form action="${linkServletNovaEmpresa}"  method = "post">
	
		Nome: <input type="text" name="nome" />
	
		<input type = "Submit" />
	
	</form>
	
</body>
</html>
```
Outra tag que pode ser utilizada é a `if`, que precede um teste de validação para executar algo.
```
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>


<html>
	<body>

		<c:if test ="${not empty empresa}">
				Empresa ${empresa} Cadastrada com sucesso!	
		</c:if>

		<c:if test ="${empty empresa}">
				Nenhuma empresa cadastrada.	
		</c:if>

	</body>
</html>
```
Outra taglib da JSTL é a fmt é utilizada para formatação e controle de datas, internacionalização, etc.
```
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ page import = "java.util.List, br.com.otavio.gerenciador.servlet.Empresa"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>


<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Java Standar Taglib</title>
</head>
<body>

	<ul>
		<c:forEach items="${empresas}" var="empresa">
				<li>${empresa.nome} - <fmt:formatDate value= "${empresa.dataAbertura}" pattern = "dd/MM/yyyy"/> </li>
		</c:forEach>
	</ul>

</body>
</html>
```
O despachador pode chamar não somente uma página html, mas também um javascript, um servlet, um jsp, etc. Uma boa prática é evitar que um Servlet chame outro Servlet, e sim que ao ser chamado, o Servlet faça sua parte, retorna uma resposta ao cliente, que irá fazer outra requisição pra outro Servlet, e assim continua. Fazemos esse redirecionamento chamando através do response o método `sendRedirect``.
```
		response.sendRedirect("listaEmpresas");
```

Podemos incluir a atualização e a exclusão para completar o CRUD, que é criar, ler, atualizar e deletar.<br>
Para remover podemos utilizar o ID (chave primária) no banco de dados, para que seja recebido do Servlet de Delete, que receberá através do getParameter.
```
@WebServlet("/removeEmpresa")
public class RemoveEmpresaServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		String paramId = request.getParameter("id");
		Integer id = Integer.valueOf(paramId);
		System.out.println(id);
		
		Banco banco = new Banco();
		banco.removeEmpresa(id);
		
	}

}
```
Quem faz o método main é o TomCat, responsável por criar uma instância do classe Servlet que será chamada. O TomCat cria apenas uma vez a instância, e apenas quando ela for chamado. Ao subirmos o servidor a instância dos servlets não é automaticamente criada, ela é criada apenas quando chamamos a primeira vez o Servlet. Quando for chamar as próximas vezes, não são criadas outras instâncias, reaproveitando a primeira instância. Esse modelo é chamado de singleton. Isso funciona claro enquanto o Tomcat está online, ao reiniciar, começa-se novamente.<br>
Isso também é chamado de inversão de controle, pois não é o meu método main que instancia o objeto, mas o TomCat.<br>
Podemos colocar o atributo `loanOnStartup` na anotação `@WebServlet`, que altera o comportamento para que o objeto seja criado ao subir o servidor.<br>
Para fazer o deploy da aplicação podemos criar um WAR, um zip que conterá todos as classes, jsp, xml, etc.