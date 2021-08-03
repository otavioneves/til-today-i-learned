Existem alguns comandos para voltar à um estado anterior do código, dependendo de até onde se deseja retornar e em qual status está o monitoramento do arquivo pelo GIT.
- Para voltar ao estado do último commit, antes do arquivo ter sido adicionado pelo `git add` no monitoramento do Git, usa-se o `git checkout --` seguido do nome do arquivo que a alteração será desfeita.
- Para voltar ao estado do último commit, após o arquivo ter sido adicionado pelo `git add` no monitoramento do Git, usa-se o `git reset HEAD ` seguido do nome do arquivo que a alteração será desfeita.
- Para desfazer as alterações feitas por qualquer commit anterior, usamos o hash do commit, que é uma tag única e específica de cada commit. Os hashs podem ser encontrados pelo comando git log. Após definirmos em qual commit queremos voltar, usamos o comando `git revert` seguido do HASH do commit.
- Para voltar no estado exato de qualquer commit anterior, após definirmos em qual estado de um exato commit queremos voltar, usamos o comando `git checkout` seguido do HASH do commit. Nesse caso, fica-se desanexado da branch atual, fica-se em uma "branch" apenas do estado atual do commit. Para poder depois commitar na branch após voltar para esse estado de um commit, é necessário após ter voltado pelo checkout, criar uma nova branch, "oficializando" esse novo ramo. Depois das alterações feitas, pode-se voltar pra master e fazer um merge ou um rebase.