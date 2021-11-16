Podemos começar a entender o padrão MVC a partir de um projeto padrão de Servlets, criando um Servlet de entrada, que receberá todas as requisições, chamado também de controlador. A função do controlador é receber as requisições e delegar as chamadas para as ações correspondentes.<br>
A ideia é que nosso controlador receba qualquer requisição para qualquer URL, através do mapeamento
```
@WebServlet("/")
public class UnicaEntradaServlet extends HttpServlet
```
Assim, podemos usar o nome da URL para definir a ação. Por exemplo, um mapeamento possível seria:
```
/listaEmpresas
/novaEmpresaForm
/removeEmpresa
```
Precisamos apenas da URL. Isso significa que devemos analisar a URL no nosso controlador para saber qual ação deveria ser chamada. O método getRequestURI(), do objeto HttpServletRequest, devolve exatamente essa informação:
```
String url = request.getRequestURI();
```
Depois de criarmos classes java para as ações, termos o modelo criado, a view é uma pasta com todas os JSP. O objetivo desse modelo e não chamar nenhum JSP através do navegador, e sempre pelo controller, que é um servlet que direciona para as ações.