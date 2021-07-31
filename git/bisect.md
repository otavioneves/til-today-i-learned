Para encontrar um estado específico do código no meio de todos os commits, utiliza-se o comando `git bisect`.<br>
Para isso, faz-se a alteração precisamos iniciar o bisect, rodando `git bisect start`.<br>
Depois de iniciado, rodamos `git biscet bad` para quando o estado do commit ainda não está com o estado que estamos buscando.<br>
Após ter marcado o bad, marca-se o good, que é o commit que procuraremos se certo estado específico está nele com `git bisect good` seguido do hash do commit. Caso ainda não esteja no estado requerido, executa-se `git bisect bad` novamente e utiliza-se o good seguido de outro hash de outro commit, buscando assim o estado requerido. Caso tenha encontrado o que estava procurando, usa-se o bisect com o good.<br>
Para finalizar o bisect, usa-se `git bisect reset`.