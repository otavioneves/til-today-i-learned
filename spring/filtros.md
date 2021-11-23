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