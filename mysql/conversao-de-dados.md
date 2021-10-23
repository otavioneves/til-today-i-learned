Podemos converter dados, como números em strings, strings em data, etc. Não mudamos o tipo do registro, o que muda é a manipulação, para poder aplicar em um código.

- DATE_FORMAT: Conversão de data em String, podendo aplicar algum tipo de conversão da data para string. (https://www.w3schools.com/mysql/func_mysql_date_format.asp)
```
SELECT DATE_FORMAT("2017-06-15", "%Y");
```

- CONVERT: comando que converte um tipo em outro:
```
SELECT CONVERT (23,3,CHAR) AS RESULTADO;
```
 - CASt: comando que converte um tipo em outro.
 <br>
Queremos construir um SQL cujo resultado seja, para cada cliente:<br>
“O cliente João da Silva faturou 120000 no ano de 2016”.<br>
Somente para o ano de 2016.<br>
```
SELECT CONCAT('O cliente ', TC.NOME, ' faturou ', 
CAST(SUM(INF.QUANTIDADE * INF.preco) AS char (20))
 , ' no ano ', CAST(YEAR(NF.DATA_VENDA) AS char (20))) AS SENTENCA FROM notas_fiscais NF
INNER JOIN itens_notas_fiscais INF ON NF.NUMERO = INF.NUMERO
INNER JOIN tabela_de_clientes TC ON NF.CPF = TC.CPF
WHERE YEAR(DATA_VENDA) = 2016
GROUP BY TC.NOME, YEAR(DATA_VENDA)C
```

