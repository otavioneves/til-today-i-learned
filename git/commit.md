Para fazer um commit, o arquivo preciso ter sido adicionado na monitoração do git através do `git add`. Com o arquivo já monitorado, usamos o comando `git commit` com a seguinte sintaxe:
```
$ git commit -m "Criando o arquivo index.html com lista inicial"
```
O comando é seguido do parâmetro `-m`, que informa ao comando que irá ser passado uma mensagem no commit, seguido da mensagem do commit entre aspas.<br><br>
Á cada modificação feita, o `git status` informa que o arquivo está pronto para ser commitado. A cada commit feito é necessário comentar o que está sendo feito, sendo que o ideal é que a quantidade de alterações sejam significativas, e algum progesso no projeto tenha sido alcançado, desse modo, deixando os log de commits limpos e de fácil utilização caso necessário.
