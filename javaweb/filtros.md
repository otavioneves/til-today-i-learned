Para tratar as preocupações de verifica usuário logado, testa permissões, faz o monitoramento, faz auditoria, tratamento de erro e transações, não utilizamos o controlador, mas sim o filtro, que é um corredor antes da porta(controlador).<br>
O Filtro consegue parar uma execução. Uma classe de filtro implementa a Classe Filter, do pacote javax.servlet.
```
public class MonitoramentoFilter implements Filter {

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
	
	}
}
```
O método doFilter recebe 3 parâmetro: request, response e FilterChain. O parâmetro chain pode chamar o método doFilter() para continuar a requisição.
```
public class MonitoramentoFilter implements Filter {

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {

		long antes = System.currentTimeMillis();
		
		chain.doFilter(request, response);		// continua executando, depois volta
		
		long depois = System.currentTimeMillis();
		
		System.out.println("Tempo de execução: " + (depois - antes));
		
	}
}
```
Precisamos também fazer o mapeamento com a anotação @WebFilter, com um URL pattern.
```
@WebFilter("/entrada")		// todas as requisições que chegarem passam pelo Filter
```
Tudo que podemos fazer em um servlet, podemos fazer em um filtro, pois também temos os atributos request e response. Podemos por exemplo pegar o parâmetro da ação para utilizá-lo dentro da lógica do filtro:
```
@WebFilter("/entrada")		// todas as requisições que chegarem passam pelo Filter
public class MonitoramentoFilter implements Filter {

	@Override
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {

		long antes = System.currentTimeMillis();
		
		String acao = request.getParameter("acao");
		
		chain.doFilter(request, response);		// continua executando, depois volta
		
		long depois = System.currentTimeMillis();
		
		System.out.println("Tempo de execução (" + acao + "): "+ (depois - antes));
		
	}
}
```
O filtro ajuda a centralizar as funcionalidades executadas na frente de toda requisição, não sendo então necessário mexer na nossa aplicação. O filtro é fácil de plugar e desplugar. Com essa facilidade, não devemos escrever lógica no controlador, já que em frameworks mais avançados esse prática não é tão simples, pois o controlador é do próprio framework. Podemos criar um filtro para esse tipo de coisa, como por exemplo, para verificar se o usuário está logado ou não.
```
@WebFilter("/entrada")
public class AutorizacaoFilter implements Filter {

	public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain chain) throws IOException, ServletException {

		HttpServletRequest request = (HttpServletRequest) servletRequest;	// utilizamos o cast para transformar algo mais genérico em uma referência mais específica, para poder usar os métodos.
		HttpServletResponse response = (HttpServletResponse) servletResponse;	// utilizando o cast
		
		String paramAcao = request.getParameter("acao");
		
		HttpSession sessao = request.getSession();
		Boolean usuarioNaoEstaLogado = (sessao.getAttribute("usuarioLogado") == null);
		Boolean naoEhUmaAcaoProtegida = paramAcao.equals("Login")|| paramAcao.equals("LoginForm");
		
		if (usuarioNaoEstaLogado && !naoEhUmaAcaoProtegida) {
			response.sendRedirect("entrada?acao=LoginForm");
			return;		// sai da execução
		}
		
		chain.doFilter(request, response);
	}

}
```
No caso de aplicar esses dois filtros, como usamos anotação, não temos controle de ordem de execução dos filtros. Para ter esse controle, precisamos definir no web.xml.
```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>gerenciador</display-name>
  <welcome-file-list>
    <welcome-file>bem-vindo.html</welcome-file>
  </welcome-file-list>
  
  <filter>
  	<filter-name>MF</filter-name>
  	<filter-class>br.com.otavio.gerenciador.servlet.MonitoramentoFilter</filter-class>
  </filter>
  
  <filter-mapping>
  	<filter-name>MF</filter-name>
  	<url-pattern>/entrada</url-pattern>
  </filter-mapping>
  
  <filter>
  	<filter-name>AF</filter-name>
  	<filter-class>br.com.otavio.gerenciador.servlet.AutorizacaoFilter</filter-class>
  </filter>
  
  <filter-mapping>
  	<filter-name>AF</filter-name>
  	<url-pattern>/entrada</url-pattern>
  </filter-mapping>
    
  
</web-app>
```
Podemos também utilizar os filtros para criar nosso controlador, e utilizar o web.xml para definir que ele rode por último.
```
	public class ControladorFilter implements Filter {
	
	
		public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain chain) throws IOException, ServletException {
	
			HttpServletRequest request = (HttpServletRequest) servletRequest;	// utilizamos o cast para transformar algo mais genérico em uma referência mais específica, para poder usar os métodos.
			HttpServletResponse response = (HttpServletResponse) servletResponse;	// utilizando o cast
			
			String paramAcao = request.getParameter("acao");	
			String nomeDaClasse = "br.com.otavio.gerenciador.acao."+ paramAcao;
			String nome;
			
			try {
				Class classe = Class.forName(nomeDaClasse); // carrega a classe com o nome e me retorna a classe
				Acao acao = (Acao) classe.newInstance();		// cast para a interface, para poder usar o nmétodo executa
				nome = acao.executa(request, response);
			} catch (ClassNotFoundException | InstantiationException | IllegalAccessException | ServletException
					| IOException e) {
				throw new ServletException(e);
			}
			
			String[] tipoEndereco = nome.split(":");		// o primeiro índice do array será se é forward ou redirect, o segundo índice do array é o endereço
			
			if (tipoEndereco[0].equals("forward")) {
				RequestDispatcher rd = request.getRequestDispatcher("WEB-INF/view/" + tipoEndereco[1]);
				rd.forward(request, response);
			} else {
				response.sendRedirect(tipoEndereco[1]);
			}
		}
	}

```
```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" id="WebApp_ID" version="4.0">
  <display-name>gerenciador</display-name>
  
  <filter>
  	<filter-name>MF</filter-name>
  	<filter-class>br.com.otavio.gerenciador.servlet.MonitoramentoFilter</filter-class>
  </filter>
  <filter-mapping>
  	<filter-name>MF</filter-name>
  	<url-pattern>/entrada</url-pattern>
  </filter-mapping>
  
  <filter>
  	<filter-name>AF</filter-name>
  	<filter-class>br.com.otavio.gerenciador.servlet.AutorizacaoFilter</filter-class>
  </filter>
  <filter-mapping>
  	<filter-name>AF</filter-name>
  	<url-pattern>/entrada</url-pattern>
  </filter-mapping>
    
  <filter>
    <filter-name>CF</filter-name>
    <filter-class>br.com.otavio.gerenciador.servlet.ControladorFilter</filter-class>
  </filter>
  <filter-mapping>
    <filter-name>CF</filter-name>
    <url-pattern>/entrada</url-pattern>
  </filter-mapping>
  
</web-app>
```
O filtro fica antes do controlador e o interceptador depois. O filtro é um componente do mundo de Servlets e se preocupa em filtrar requisições (é ligado ao mundo web), enquanto um interceptador "filtra" chamadas de ações ou outros métodos. Os interceptadores são específicos do framework (por exemplo, Spring) e até funciona sem Servlets.