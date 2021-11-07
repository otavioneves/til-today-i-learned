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
Para acessar uma página do Tomcat utilizamos protocolo://ip:porta/contexto/recurso. No caso da classe, utilizamos o nome colocado na anotação da Classe.