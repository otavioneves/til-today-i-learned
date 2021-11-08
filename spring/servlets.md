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
No lado do Servlet, precisamos chamar o JSP que possuí o código HTML.