Para apresentar os dados de uma requisição não podemos utilizar sempre o HTML (no caso, o JSP), pois o HTML é mais voltado ao navegador, por isso, podemos utilizar o JSON ou XML. JSON ou XML é um grande string, aonde cada cliente irá interpretar do seu jeito. Os frameworks de Javascript também não consomem HTML, mas recebem o JSON ou XML e geram o HTML. Os Web Services usa o protocolo HTTP para chamar alguma funcionalidade remotamente e devolve os dados em JSON ou XML.<br>
Os JSON utiliza chaves, e as chaves-valor ("title":"example glossary"). Podemos também definir qual conteúdo devolveremos, conforme abaixo:
```
@WebServlet("/empresas")
public class EmpresasService extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

		List<Empresa> empresas = new Banco().getEmpresas();
	
		Gson gson = new Gson();
		String json = gson.toJson(empresas);
	
		response.setContentType("application/json");
		response.getWriter().print(json); 		// imprime o json na saída, através de um fluxo de string.
		
	}

}
```
Ao acessar `http://localhost:8080/gerenciador/empresas`, é retornado em JSON, com um array de strings.
```
[{"id":2,"nome":"Caelum","dataAbertura":"Nov 23, 2021, 12:02:27 AM"},{"id":1,"nome":"Alura","dataAbertura":"Nov 23, 2021, 12:02:27 AM"}]
```
<br>
Podemos também utilizar o XML, no caso através da biblioteca Xstream:
```
@WebServlet("/empresas")
public class EmpresasService extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

		List<Empresa> empresas = new Banco().getEmpresas();
	
		XStream xstream = new XStream();
		String xml = xstream.toXML(empresas);
	
		response.setContentType("application/xml");
		response.getWriter().print(xml); 		// imprime o xml na saída, através de um fluxo de string.
		
	}

}
```