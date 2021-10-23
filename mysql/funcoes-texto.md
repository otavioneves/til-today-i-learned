[Documentação](https://www.w3schools.com/sql/)<br>
[W3 Schools](https://www.w3schools.com/sql/>)<br>
Temos alguns tipos de funções no MySQL, uma delas é:

### Funções de texto:
- CONCAT: concatenar strings
```
SELECT CONCAT("SQL ","Tutorial ", "is "," fun!") AS CONCATENATEDSTRING;
```
- LTRIM: retira espaços à esquerda do string.
```
SELECT LTRIM("      SQL Tutorial") AS LEFTTRIMMEDSTRING;
```
- RTRIM: retira espaço à direita do string.
```
SELECT RTRIM("SQL Tutorial      ") AS RIGHTTRIMMEDSTRING;
```
- TRIM: retira espaço à direita e à esquerda do string.
```
SELECT TRIM("     SQL Tutorial      ") AS TRIMMEDSTRING;
```
- LCASE: deixa todo String em minúsculo;
```
SELECT LCASE("SQL Tutorial is FUN!");
```
- LOWER: deixa todo String em minúsculo;
```
SELECT LOWER("SQL Tutorial is FUN!");
```
- UCASE: deixa todo String em maíusculo;
```
SELECT UCASE("SQL Tutorial is FUN!");
``` 
- UPPER: deixa todo String em maíusculo;
```
SELECT UPPER("SQL Tutorial is FUN!");
``` 
- SUBSTRING: retirar um pedaço de um string, a partir de um string, uma posição inicial do novo substring e o tamanho do novo substring.
```
SELECT SUBSTRING("SQL Tutorial",5,3) AS ExtractString;
```
- LENGTH: retorna o tamanho do String.
```
SELECT LENGHT("SQL Tutorial) AS LENGTHOFSTRING;
```
- INSTR: verifica se uma string está dentro de outra.
```
INSTR(STRING1, STRING2);
```
- Aplicação real:
```
SELECT NOME, CONCAT(ENDERECO_1, ' ', BAIRRO, ' ', CIDADE, ' ', ESTADO) AS COMPLETO
FROM tabela_de_clientes
```
