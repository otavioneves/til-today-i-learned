Para guardar alguma informação durante uma sessão, por exemplo, guardar o usuário logado após feito o login, utilizamos as HttpSessions. Os objetos gerados pelo atributo request ou response valem por apenas uma requisição. Ao acabar a requisição, os dados são perdidos. A identificação que mantém esse registro é a SessionID. O JSessionID é enviado junto aos Cookies.<br>
Quando o servidor vê a requisição pela primeira vez, ele cria essa seção, criando um objeto HtppSession e um valor associado, que é o ID. Podemos utilizar esse ID e o objeto criado no nosso código, para estabelecer uma sessão.
```
HttpSession sessao = request.getSession();
sessao.setAttribute("usuarioLogado", usuario);
```

O HttpSession é utilizado para guardar informações do usuário durante uma requisição.
