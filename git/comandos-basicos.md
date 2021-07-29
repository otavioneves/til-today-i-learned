Para navegar até um repositório usa-se ou o bash do Git ou do o bash do Linux/MAC para ir até o diretório, utilizando o comando `cd`

```
$ cd/Documents/project1
```

Para inicializar esse repositório no Git, de modo que a partir deste comando o Git poderá gerenciar as modificações realizadas nos arquivos, é o comando utilizado é o `git init`

```
$ git init
```

Para verificar o estado do repositório, como por exemplo qual é a branch, quantos commits foram feitos e os arquivos, entre outroas informações, utiliza-se o comando `git status`
Os arquivos denominados como "Untracked files" são arquivos que ainda não estão sendo monitorados no GIT.
```
$ git status
```
Algumas informações importantes aparecem ao executar o comando `git status`, são elas:<br>
- HEAD: Estado atual do código;
- Working tree: Local onde os arquivos realmente estão sendo armazenados e editados
- index: Local onde o Git armazena o que será commitado, ou seja, o local entre a working tree e o repositório Git em si.<br>
Para o arquivo passar à ser monitorado, utilizamos o `git add` e o nome do arquivo. Ao utilizar o "." após o comando, o Git passa a monitorar todos os arquivos do repositório.
O arquivo passa à poder ser commitado.
```
$ git add index.html
```
O comando `git add` "serve para começar a rastrear arquivos e também para outras coisas, como marcar arquivos que estão em conflito de mesclagem como resolvidos.Pode ser útil pensar nesse comando mais como “adicione este conteúdo ao próximo commit”." Documentação do GIT SCM.<br>
Quando um arquivo é alterado após ser colocado no stage, o arquivo fica constando como stage e unstage, pois o que está pronto para ser commitado é o que foi adicionado pelo `git add`, sendo necessário refazê-lo com a versão nova.
