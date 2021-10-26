Para projetar um banco de dados precisamos dos seguintes requisitos:
- Entendimento das regras de negócio;
- Efetuar atividades de entrevistas e reuniões;
- Desenho de modelo mais fiel à realidade.
Após ter levantado essas informação temos um modelo conceitual, construindo um diagrama de Entidade e Relacionamento, estabalecendo uma cardinalidade entre as entidades. Exemplo:
- "Um VENDEDOR realiza uma VENDA, um CLIENTE está contido em uma VENDA, a VENDA possuí ITENS_VENDIDOS, e os ITENS_VENDIDOS possuem PRODUTOS".
- "1 vendedor pode estar realionado à N VENDAS, assim com o cliente. Já a VENDA é sempre única, e possui N ITENS_VENDIDOS. Cada ITENS_VENDIDOS possuí 1 PRODUTOS".
<br>
Após isso, estabelecemos as características de cada entidade, aonde cada tabela recebe as informações dos campos, tipos, etc. Os diagramas viram então tabelas, onde definimos chaves primárias e os relacionamentos com as chaves estrangeiras.<br>
Para construir através das ferramentas CASE, aonde desenhamos de maneira gráfica as tabelas e a ferramenta cria a tabela. Podemos também fazer pelo workbench, sem nenhum problema, utilizando o comando CREATE DATABASE.
```
CREATE DATABASE vendas_sucos;
```
Para apagar o banco, podemos usar o comando DROP DATABASE IF EXISTS
```
DROP DATABASE IF EXISTS vendas_sucos;
```
Podemos criar ou apagar também pelo assistente do workbench.<br>

### Tabela
Para criar tabela, seguimos a seguinte sintaxe:
```
CREATE TABLEA nomedatabela(

nomedocampo tipodocampo seaceitaounãonulo
nomedocampo tipodocampo seaceitaounãonulo
nomedocampo tipodocampo seaceitaounãonulo
...
nomedocampo tipodocampo seaceitaounãonulo

PRIMARY KEY(nomesdocamposPKseparadosporvirgula)
)
```
Para apagar a tabela:
```
DROP TABELA nomedatabela
```
Para mudar o nome de uma coluna podemos utilizar o comando ALTER TABLE:
```
ALTER TABLE vendedores RENAME COLUMN DATA_ADIMISSAO TO DATA_ADMISSAO;
```
<br>
Para criarmos um chave estrangeira, podemos utilizar também o ALTER TABLE:
```
ALTER TABLE tabela_de_vendas ADD CONSTRAINT FK_CLIENTES FOREIGN KEY (CPF) REFERENCES clientes (CPF);
```
<br>
Para alterar o nome de uma tabela utilizamos o comando ALTER TABLE:
```
ALTER TABLE tabela_de_vendas RENAME notas;
```
<br>
Para verificarmos o banco em formato de Diagrama usamos a ferramenta Reverse Enginner. Podemos também exportar a criação da nossa tabela, saindo um arquivo que vem com todos os comandos para criação de uma dada tabela, em File > Export > Forward Enginner SQL CREATE Script.

### Inserir dados na tabela
O comando utilizar para adicionar campos na tabela é através do comando INSERT.
```
INSERT INTO tabela (campos separados por virgulas)
VALUES (valores dos campos a serem incluidos );
```
```
INSER INTO tabela (campos da tabela separados por virgula)
VALUES() (valores dos campos a serem incluidos ),(valores dos campos a serem incluidos ),..., (valores dos campos a serem incluidos );
```
Exemplo:
```
INSERT INTO PRODUTOS (CODIGO, DESCRITOR, SABOR, TAMANHO, EMBALAGEM, PRECO_LISTA)
VALUES ('1040107','Light - 350 ml - Melância','Melância','350ml','Lata',4.56);
```
```
INSERT INTO PRODUTOS (CODIGO, DESCRITOR, SABOR, TAMANHO, EMBALAGEM, PRECO_LISTA)
VALUES
('1040108','Light - 350 ml - Graviola','Graviola','350ml','Lata',4.00), 
('1040109','Light - 350 ml - Açaí','Açaí','350ml','Lata',5.60);
```

### Importar dados de outro banco
Para importar dados de outro banco, podemos também utilizar dados importados de outra tabela presente em outro banco. Para isso utilizamos o INSERT INTO que recebe uma consulta.
```
INSERT INTO PRODUTOS (CODIGO, DESCRITOR, SABOR, TAMANHO, EMBALAGEM, PRECO_LISTA)
SELECT CODIGO_DO_PRODUTO AS CODIGO, NOME_DO_PRODUTO AS DESCRITOR, SABOR , TAMANHO, EMBALAGEM, PRECO_DE_LISTA AS PRECO_LISTA
FROM sucos_vendas.tabela_de_produtos
WHERE CODIGO_DO_PRODUTO NOT IN ( SELECT CODIGO FROM PRODUTOS);
```

### Alterando dados na tabela
Podemos alterar os dados de uma tabela com o comando UPDATE.
```
UPDATE nome da tabela SET nome do campo = valor
WHERE condição
```
```
UPDATE produtos SET PRECO_LISTA=5 WHERE CODIGO = '1000889';     // alterando 1 campo de 1 registro

UPDATE produtos SET EMBALAGEM = 'PET', TAMANHO = '1 Litro', DESCRITOR = 'Sabor da Montanha - 1 Litro - Uva' WHERE CODIGO = '1000889';       // alterando 3 campos de 1 registro

UPDATE produtos SET PRECO_LISTA = PRECO_LISTA * 1.10 WHERE SABOR = 'Maracujá'; alterando 1 campo de mais de um registro
```

Podemos usar também UPDATE através do comando SELECT.
```
UPDATE CLIENTES A INNER JOIN VENDEDORES B
ON A.BAIRRO = B.BAIRRO
SET A.VOLUME_COMPRA = A.VOLUME_COMPRA * 1.30
```

### Excluir dados da tabela
```
DELETE FROM nome da tabela WHERE condicao;

DELETE FROM produtos WHERE TAMANHO = '1 Litro';
```
