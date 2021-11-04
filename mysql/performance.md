Um dos principais fatores que influenciam a performance é o tempo de consulta. Para saber o tempo de cada consulta podemos utilizar o comando `EXPLAIN`, que pode receber alguns argumentos, como o `FORMAT=JSON.`
Uma outra forma de ganhar performance é utilizar indices.
### Indices em tabelas do tipo MYISAM
- Cria uma estrutura a parte para índices PK e não PK;
- Nesta estrutura a coluna do índice é ordenada e tem como referência a posição da linha da tabela original;
- Implementa índices HASH e B-TREE.

### Indices em tabelas do tipo INNODB
- A tabela orignal já é ordenada pela PK;
- Os índices não PK possuem estruturas a parte one a coluna do índice é ordenada e tem como referência o valor da PK;
- Implementa somente índices B-TREE.

HASH e B-TREE são diferentes algoritmos de busca em lista ordenada.