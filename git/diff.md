Para verificar a diferença entre dois commits, utiliza-se o comando `git diff` seguido dos hashs à serem comparados, separados por ponto ponto.<br>
```
$ git diff 1234567..1234567
```
Com esse comando, é possível também verificar quais alterações foram feitas, em relação ao arquivo original, antes de adicionar as alterações pelo `git add`. Para isso, executa-se apenas o `gi diff`.<br>
Resumindo: com o git diff é possível verificar a diferença dos arquivos de dois commits e a diferença do arquivo para o original, antes de commitar.