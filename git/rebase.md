Para unir o trabalho de uma branch para a master, sem criar um commit de merge, utiliza-se o `git rebase`.<br>
O rebase traz os commits da branch para a master, deixando os em sequência, melhorando assim o log.<br><br>
A sintaxe do comando é, primeiramente ir para master, através do `git checkout master`, e utilizar o comando `git rebase` seguido do nome da branch.