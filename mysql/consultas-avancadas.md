Para verificarmos tudo que temos em um banco, podemos utilizar o MySQL WorkBench através do Reverse Enginer, na opção Database. Esse atalho faz uma Engenharia Reversa com a tabela que selecionarmos, mostrando os campos de cada tabela, suas chaves primárias e as chaves entrangeiras. Com essa ferramenta podemos conhecer o banco de dados antes de começar a fazer as consultas.
### Aplicações sobre os filtros
- Expressões condicionais com NOT, para consultas: podemos utilizar o NOT na frente da expressão para inverter o resultado da condição.
```
SELECT * FROM tabela_de_produtos WHERE NOT (SABOR = 'MANGA' OR TAMANHO = '470 ml');
```
- Expressões condicionais com IN, para consultas: podemos utilizar o IN para selecionar os registros que contenham os itens colocados.
```
SELECT * FROM tabela_de_clientes WHERE CIDADE IN ('Rio de Janeiro', 'São Paulo');
``` 
- Expressões condicionais com LIKE, para consultas: podemos utilizar o LIKE para selecionar os registros que contenham uma condição que passamos entre `%%`.
```
SELECT * FROM tabela_de_produtos WHERE SABOR LIKE ('%Maça%');           // tudo que tenha Maça

SELECT * FROM tabela_de_produtos WHERE SABOR LIKE ('%Maça');            // tudo que termina com Maça

SELECT * FROM tabela_de_produtos WHERE SABOR LIKE ('%Maça');            // tudo que começa com Maça
```

### Aplicações sobre a visualização
- DISTINCT: irá retornar somente linhas com valore diferentes, como se fosse um retirar duplicatas, mostra as combinações de registros que não se repetem. O comando vem após o SELECT.
```
SELECT DISTINCT EMBALAGEM, TAMANHO FROM tabela_de_produtos;

SELECT DISTINCT EMBALAGEM, TAMANHO, SABOR FROM tabela_de_produtos WHERE SABOR = 'Laranja';      // podemos utilizar os filtros também
```
- LIMIT: limita os números de linhas exibidas, que é aplicado no final da linha.
```
SELECT * FROM tabela_de_produtos LIMIT 4;
```
Para pegarmos não só os primeiros, podemos colocar um número de início, seguido do número de registros que serão listado.
```
SELECT * FROM tabela_de_produtos LIMIT 2,4;     // a partir da posição 2, seleciona os próximos 4.
```
- ORDER BY: apresenta o resultado da consulta ordenado pelo determinado no ORDER BY. Podemos fazer a ordenação crescente (ASC) ou descrescente (DESC). O comando é colocado no final da linha do comando.
```
SELECT * FROM tabela_de_produtos ORDER BY PRECO_DE_LISTA;       // CRESCENTE, ORDENAÇÃO PADRÃO, NÃO PRECISA COLOCAR NADA.

SELECT * FROM tabela_de_produtos ORDER BY PRECO_DE_LISTA DESC;      // DESCENDENTE

SELECT * FROM tabela_de_produtos ORDER BY EMBALAGEM, PRECO_DE_LISTA;        // CRITÉRIO COMPOSTO

SELECT * FROM tabela_de_produtos ORDER BY EMBALAGEM DESC, PRECO_DE_LISTA ASC;       // CRITÉRIO COMPOSTO COM ASC E DESC
```
- Agrupar o resultado: apresenta o resultado agrupando valores númericos por uma chave de critério. Podemos ao fazer essa junção em campos númericos, podemos aplicar alguns cálculos.
A sintaxe é: SELECT campos FROM tabela GROUP BY campo
```
SELECT ESTADO, SUM(LIMITE_DE_CREDITO) AS LIMITE_TOTAL FROM tabela_de_clientes GROUP BY ESTADO;      // selecionando o limite de créditos de cada estado da tabela

SELECT EMBALAGEM, MAX(PRECO_DE_LISTA) AS MAIOR_PRECO FROM tabela_de_produtos GROUP BY EMBALAGEM;        // selecionando o maior preço de cada embalagem

SELECT EMBALAGEM, COUNT(*) FROM tabela_de_produtos GROUP BY EMBALAGEM;      // contando a quantidade de cada produto por embalagem

SELECT BAIRRO, SUM(LIMITE_DE_CREDITO) AS LIMITE FROM tabela_de_clientes WHERE CIDADE = 'Rio de Janeiro'GROUP BY BAIRRO;        // selecionando o limite de créditos de cada bairro do estado do rio janeiro

SELECT BAIRRO, SUM(LIMITE_DE_CREDITO) AS LIMITE FROM tabela_de_clientes WHERE CIDADE = 'Rio de Janeiro'GROUP BY BAIRRO ORDER BY BAIRRO;         // grupando, ordenando e filtrando
```
Podemos aplicar: SUM (soma), MAX (máximo), MIN (mínimo), AVG (média), COUNT (conta ocorrências). Podemos também utilizar esses comandos sem utilizar o GROUP BY, ficando algo como: SELECT SUM(Y) FROM TAB, que somaria tudo do Y.<br>
Podemos também ter no GROUP BY em mais de um campo.
```
SELECT ESTADO, BAIRRO, SUM(LIMITE_DE_CREDITO) AS LIMITE FROM tabela_de_clientes WHERE CIDADE = 'Rio de Janeiro'GROUP BY ESTADO, BAIRRO;
```

- HAVING: esse comando é um filtro que é aplicado sobre um SELECT, ou seja, uma condição que se aplica ao resultado de uma agregação.
```
SELECT ESTADO, SUM(LIMITE_DE_CREDITO) AS SOMA_LIMITE FROM tabela_de_clientes GROUP BY ESTADO HAVING SUM(LIMITE_DE_CREDITO)>900000;      // selecionando o estado com as somas de limite de credito de cada um, mostrando apenas os que tem soma maior de 900.000,00
```

- CASE: fazemos um teste em um ou mais campos e, dependendo do resultado, teremos um ou outro valor. CASE WHEN condicao THEN valor ELSE valorelse END AS nomedonovocampo FROM tabela.
```
SELECT NOME_DO_PRODUTO, PRECO_DE_LISTA,
CASE
	WHEN PRECO_DE_LISTA >= 12 THEN 'PRODUTO CARO'
    WHEN PRECO_DE_LISTA >= 7 AND PRECO_DE_LISTA <12 THEN 'PRODUTO EM CONTA'
	ELSE 'PRODUTO BARATO'
    END AS STATUS_PRECO
FROM tabela_de_produtos;
```
```
SELECT EMBALAGEM,
CASE
	WHEN PRECO_DE_LISTA >= 12 THEN 'PRODUTO CARO'
    WHEN PRECO_DE_LISTA >= 7 AND PRECO_DE_LISTA <12 THEN 'PRODUTO EM CONTA'
	ELSE 'PRODUTO BARATO'
    END AS STATUS_PRECO, AVG(PRECO_DE_LISTA) AS PRECO_MEDIO
FROM tabela_de_produtos
WHERE SABOR = 'Manga'
GROUP BY EMBALAGEM,
CASE
	WHEN PRECO_DE_LISTA >= 12 THEN 'PRODUTO CARO'
    WHEN PRECO_DE_LISTA >= 7 AND PRECO_DE_LISTA <12 THEN 'PRODUTO EM CONTA'
	ELSE 'PRODUTO BARATO'
END
ORDER BY EMBALAGEM;
```