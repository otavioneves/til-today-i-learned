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
Depois de criarmos classes java para as ações, termos o modelo criado, a view é uma pasta com todas os JSP. O objetivo desse modelo e não chamar nenhum JSP através do navegador, e sempre pelo controller, que é um servlet que direciona para as ações.<br>
O padrão MVC são 3 camadas que são:
- Controller: uma entrada única que recebe todas as requisições do navegador. Ele possui o servlet de entrada e as ações (classes java que implementam uma interface que possui o método executa). A ação também define qual modelo irá utilizar. A ação também define o nome que será chamado no navegador, apesar de elas apenas definirem se é forward ou redirect.
- Modelo: modelo que possui a camada de persistência.
- View: o view é a camada que não sabe de onde vem os dados, apenas os renderiza e os apresenta. Nessa camada é aonde está presente os JSP, que são chamados pelo Controller.

Cada ação possui somente um método, que se chama executa (execute). Também poderíamos ter chamado esse método de rode (run) ou call, não faria diferença, mas sempre o objetivo desse método é encapsular a execução da ação. A nossa interface Acao padronizou a assinatura do método para todas as ações seguirem o mesmo comportamento.<br>
Repare também que, só pelo nome do método, não sabemos o que está sendo executado. Para tal, precisamos olhar o nome da classe. Isso também não importa para o controlador, o que importa é ter o método executa. Seguindo esse padrão, conseguimos delegar as chamadas do controlador central para as ações. Todas as nossas classes seguem o padrão Command.