[Documentação](https://www.w3schools.com/sql/)<br>
[W3 Schools](https://www.w3schools.com/mysql/mysql_ref_functions.asp)<br>
Temos alguns tipos de funções no MySQL, uma delas é:

### Funções de data:
- ADDDATE: adiciona sobre a data um intervalo de data;
```
SELECT ADDDATE("2017-06-15", INTERVAL 10 DAY);
```
- ADDTIME: adiciona sobre o tempo um intervalo de tempo, necessita do formato timestamp;
```
SELECT ADDTIME("2017-06-15 09:34:21", "2");
```
- CURDATE: retorna a data corrente;
```
SELECT CURDATE();
```
- CURRENT-TIME;
- CURRENT-DATE;
- CURRENT-TIMESTAMP;
- DATEDIFF: diferença em dias de datas;
```
SELECT DATEDIFF("2017-06-25", "2017-06-15");
```
- DAYNAME;
- DAY;
- MONTH;
- MONTHNAME;
- YEAR;

- Aplicação Real:
```
SELECT NOME, TIMESTAMPDIFF (YEAR, DATA_DE_NASCIMENTO, CURDATE()) AS    IDADE
FROM  tabela_de_clientes
```
