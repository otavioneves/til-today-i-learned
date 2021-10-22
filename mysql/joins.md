A estrutura de JOINs permite juntar uma ou mais tabelas através de um mais campos em comum.
- INNER JOIN: traz todo mundo que tem correspondências nas duas tabelas.
```
SELECT A.nome, B.hobby
FROM tabela1 A INNER JOIN tabela2 B
ON A.identificador = B.identificador;
```
- LEFT JOIN: trazer todo mundo da esquerda e só os correspodentes da direita. Os que não tiverem correspondência vem como null.
```
SELECT A.nome, B.hobby
FROM tabela1 A LEFT JOIN tabela2 B
ON A.identificador = B.identificador;
```
- RIGHT JOIN: trazer todo mundo da direita e só os correspodentes da esquerda. Os que não tiverem correspondência vem como null.
```
SELECT A.nome, B.hobby
FROM tabela1 A RIGHT JOIN tabela2 B
ON A.identificador = B.identificador;
```
- FULL JOIN: trazer todo mundo da direita e da esquerda. Os campos que não tiverem correspondência tanto de cá pra lá, quanto de lá pra cá, vem como null. Não funciona no MySQL
```
SELECT A.nome, B.hobby
FROM tabela1 A FULL JOIN tabela2 B
ON A.identificador = B.identificador;
```
- CROSS JOIN: retorna o produto cartesiano das duas tabelas, ou seja, todos as combinações possíveis entre os campos selecionados.
```
SELECT A.nome, B.hobby
FROM tabela1 A, tabela2 B;
```
<br>
Exemplos:
```
SELECT A.MATRICULA, A.NOME, COUNT(*)
FROM tabela_de_vendedores A INNER JOIN notas_fiscais B
ON A.MATRICULA = B.MATRICULA
GROUP BY A.MATRICULA, A.NOME;
```
```
SELECT YEAR(DATA_VENDA), SUM(QUANTIDADE * PRECO) AS FATURAMENTO
FROM notas_fiscais NF INNER JOIN itens_notas_fiscais INF
ON NF.NUMERO = INF.NUMERO
GROUP BY YEAR(DATA_VENDA);

// Faturamento anual da empresa
```
```
SELECT DISTINCT A.CPF, A.NOME, B.CPF
FROM tabela_de_clientes A LEFT JOIN notas_fiscais B
ON A.CPF = B.CPF
WHERE B.CPF IS NULL;

// traz os clientes que nunca fizeram nenhuma compra, ficará com null
```
```
SELECT tabela_de_vendedores.BAIRRO, tabela_de_vendedores.NOME, tabela_de_vendedores.DE_FERIAS, tabela_de_clientes.BAIRRO, tabela_de_clientes.NOME
FROM tabela_de_vendedores, tabela_de_clientes;

// CROSS JOIN
```

- UNION: para juntar duas consultas usamos o UNION. PAra juntar precisamos de mesmo nomes de colunas e mesmos tipos de colunas. Quando fizemos UNION é aplicado o DISTINCT automaticamente. Se usarmos o UNION ALL, o DISTINCT não é aplicado.
```
SELECT DISTINCT BAIRRO FROM tabela_de_clientes
UNION
SELECT DISTINCT BAIRRO FROM tabela_de_vendedores;
```
```
SELECT DISTINCT BAIRRO FROM tabela_de_clientes
UNION ALL
SELECT DISTINCT BAIRRO FROM tabela_de_vendedores;
```

```
SELECT tabela_de_vendedores.BAIRRO, tabela_de_vendedores.NOME, tabela_de_vendedores.DE_FERIAS, tabela_de_clientes.BAIRRO, tabela_de_clientes.NOME
FROM tabela_de_vendedores LEFT JOIN tabela_de_clientes
ON tabela_de_vendedores.BAIRRO = tabela_de_clientes.BAIRRO
UNION
SELECT tabela_de_vendedores.BAIRRO, tabela_de_vendedores.NOME, tabela_de_vendedores.DE_FERIAS, tabela_de_clientes.BAIRRO, tabela_de_clientes.NOME
FROM tabela_de_vendedores RIGHT JOIN tabela_de_clientes
ON tabela_de_vendedores.BAIRRO = tabela_de_clientes.BAIRRO;
```