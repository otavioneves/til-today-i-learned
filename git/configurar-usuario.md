Para configurar o usuário no git, usa-se o `git config` com o argumento `--local`, para alterar o usuário de um projeto, e o parâmetro `--global` para alterar o usuário de toda a máquina, como por exemplo:

```
git config --local user.name "Otavio Neves"
git config --local user.email "email@outlook.com"
```
```
git config --global user.name "Otavio Neves"
git config --global user.email "email@outlook.com"
```
Para verificar qual o usuário utiliza-se comando `git config` com o argumento `user.mail`, para o e-mail, e o `user.name`, para o nome.