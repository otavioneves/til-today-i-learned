Para salvar uma alteração aonde não se deseja ainda executar um commit, utiliza-se o `git stash`, para salvar de maneira temporária as alterações feitas.<br>
No caso de precisar apenas trazer as alterações, utiliza-se o `git apply` seguido do código do stash, encontrado através da lista do `git stash list`.<br>
Para depois apagar esse stash, pode-se utilizar o comando `git stash drop` seguido do código do stash.<br>
Para trazer de volta essa alteração, utiliza-se o `git stash pop`.O pop traz as alterações, aplica e apaga o stash. 