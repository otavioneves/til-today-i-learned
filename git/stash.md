Para salvar uma alteração aonde não se deseja ainda executar um commit, utilizamos o `git stash`, para salvar de maneira temporária as alterações feitas.<br>
No caso de precisar apenas trazer as alterações, utilizamos o `git apply` seguido do código do stash, encontrado através da lista do `git stash list`.<br>
Para depois apagar esse stash, podemos utilizar o comando `git stash drop` seguido do código do stash.<br>
Para trazer de volta essa alteração, utilizamos o `git stash pop`.O pop traz as alterações, aplica e apaga o stash. 