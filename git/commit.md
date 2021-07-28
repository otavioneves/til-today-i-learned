Para o arquivo passar à ser monitorado, utilizamos o `git add` e o nome do arquivo. Ao utilizar o "." após o comando, o Git passa a monitorar todos os arquivos do repositório.
O arquivo passa à poder ser commitado.
```
$ git add index.html
```
Para fazer um commit, o arquivo preciso ter sido adicionado, ou atualizado, na monitoração do git através do `git add`. Com o arquivo já monitorado e atualizado, usamos o comando `git commit` com a seguinte sintaxe:
```
$ git commit -m "Criando o arquivo index.html com lista inicial"
```
O comando é seguido do parâmetro `-m`, que informa ao comando que irá ser passado uma mensagem no commit, seguido da mensagem do commit entre aspas.<br><br>
Á cada modificação feita no arquivo, o `git status` informa que as alterações não foram commitadas, aparecendo na seção “Changes not staged for commit”.<br><br>
A cada commit feito é necessário comentar o que está sendo feito, sendo que o ideal é que a quantidade de alterações sejam significativas, e algum progesso no projeto tenha sido alcançado, desse modo, deixando os log de commits limpos e de fácil utilização caso necessário.<br><br>

O comando `git add` "serve para começar a rastrear arquivos e também para outras coisas, como marcar arquivos que estão em conflito de mesclagem como resolvidos.Pode ser útil pensar nesse comando mais como “adicione este conteúdo ao próximo commit”." Documentação do GIT SCM.<br><br>
Quando um arquivo é alterado após ser colocado no stage, o arquivo fica constando como stage e unstage, pois o que está pronto para ser commitado é o que foi adicionado pelo `git add`, sendo necessário refazê-lo com a versão nova.<br>
O ideal é commitar sempre que alguma função for criada, ou algum bug for resolvido, etc. Ou seja, quando algum marco importante do projeto seja alcançado.
