Para verificar o histórico usamos o `git log`. Esse comando apresenta algumas informações como o Hash dos commits, o autor, a data e o título do commit.<br>
Algumas outras maneiras de ver esse log, são utilizando alguns parâmetros após o `git log`:
- `--oneline`: apresenta algumas informações dos commits no histórico em apenas uma linha;
- `-p`: apresenta mais informações dos commits no histórico, como as alterações feitas.
- `--author` seguido do nome: apresenta commits de determinado autor;
- `--since` seguido do período em inglês: apresenta os commits desde um determinado período.
- `--preety` seguido de =format:% e o argumento: apresenta o log de maneira formatada conforme os argumentos passsados.
Outros argumentos úteis estão disponíveis na página [git log cheatseet da devhints.io](https://devhints.io/git-log).<br>
Utilizando o `git log --graph`, podemos ver os commits, os commit das branchs separadas e os commits de merge, de uma maneira gráfica.