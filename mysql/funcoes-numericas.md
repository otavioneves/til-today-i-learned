[Documentação](https://www.w3schools.com/sql/)<br>
[W3 Schools](https://www.w3schools.com/mysql/mysql_ref_functions.asp)<br>
Temos alguns tipos de funções no MySQL, uma delas é:

### Funções Numéricas:
- ABS: valor absoluto;
- AVG: calcula média;
- SUM: soma;
- MAX: máximo;
- MIN: mínimo;
- CEILING arrendodamento;
- FLOOR: arrendodamento;
- ROUND: arrendodamento;
- SQRT: raiz quadrada;

- Aplicação real: Na tabela de notas fiscais temos o valor do imposto. Já na tabela de itens temos a quantidade e o faturamento. Calcule o valor do imposto pago no ano de 2016 arredondando para o menor inteiro.
```
SELECT YEAR(DATA_VENDA), FLOOR(SUM(IMPOSTO * (QUANTIDADE * PRECO))) 
FROM notas_fiscais NF
INNER JOIN itens_notas_fiscais INF ON NF.NUMERO = INF.NUMERO
WHERE YEAR(DATA_VENDA) = 2016
GROUP BY YEAR(DATA_VENDA)
```