O banco de dados é uma espaço no disco aonde armazenaremos os dados. Dentro do banco de dados temos algumas entidades, como a tabela, que é a entidade principal do banco de dados. Quando criamos uma tabela definimos as informação de quantidade de colunas e os tipos dos campos de cada coluna. Ao definirmos esse tipo, todos os campos dessa coluna tem que ser necessariamente do mesmo tipo.<br>
Uma tabela tem quantidade definida de colunas (campos), mas indefinida de linhas (registros), ficando limitadas pelo tamanho do disco ou pela política de crescimento desse banco.<br>
Um outro conceito é a chave primária, aonde definimos uma coluna que irá controlar para que não existam elementos duplicados na tabela, como o CPF, ou seja, só poderemos ter uma linha com cada CPF. Podemos usar chave primária composta, que define uma composição de dois campos para gerar uma condição para não ter elementos duplicados.<br>
Outro conceito é a chave estrangeira, que define uma relação de uma tabela com outra, mantendo uma ligação e mantendo alguns critérios como: não ter algo em uma tabela que não tenha na outra. Isso é a base do banco de dados relacional, aonde as tabelas tem relações entre si, garantindo a integridade dos dados, por exemplo: não poderei ter uma venda na tabela de vendas para um cliente que não esteja previamente cadastrado na tabela de cliente.<br>
A tabela pode ter também índices, que é um campo que facilita buscas no banco de dados, como buscar por nome, aonde o índice pode indicar algo como a primeira letra do nome.<br>
Um grupo de tabelas é chamado de esquema, como se fosse um assunto, que não necessiariamente define ligações exclusivas, podendo uma tabela se relacionar com tabelas de outros esquemas.<br>
Um banco de dados também possui uma View, que é uma consulta, ou query, que faz consultas em uma ou mais tabelas e juntam essas informações específicas em uma tabela só, gerando uma visão.<br>
Podemos fazer consultas na base de dados, consultando as informações de uma ou mais tabelas. Quando fazemos a consulta de mais de uma tabela, é chamado de join, que junta as tabelas através de um critério. Ao fazer as consultas podemos utilizar filtros, como clientes masculinos, ou clientes que moram na região sul. Podemos depois transformar ela numa view.<br>
Internamente o banco de dados possui os Procedures, que são uma solução para resolver o problema de estruturação da linguagem SQL, ou seja, são uma linguagem nativa do banco de dados para executar lógicas, funções e algoritmos que não são possíveis pela linguagem SQL. Podemos por exemplo criar uma função com os parâmetros dos campos, e depois utilizar esse resultado dentro de um comando de consulta. O MySQL já possuí procedures padrões como tirar espaços em brancos, transformar maiusculas em minúsculas, fazer calculos complexos de datas, calculos números, etc. Podemos também construir nossa própria função.<br>
Também existem os Trigger, que são avisos que são emitidos quando algo acontecer no banco de dados ou na tabela, como por exemplo: me avise caso alguém insira ou exclua algo da tabela. Podemos, por exemplo, unir com uma procedure ou com um comando SQL, que será executada assim que a condição da Trigger for satisfeita. Por exemplo: temos uma tabela de cliente e uma tabela de taxas, onde todo cliente cadastrado é criado uma tabela de taxas para esse cliente, começando com uma taxa zero e podemos criar uma trigger que ao incluir alguém no cliente, vai na tabela de taxa de crie com uma taca default.

A estrutura básica de um banco de dados é a tabela. As colunas tem determinados tipos, que ao serem criados, não podem mudar, sendo que todos os valores dessa coluna tem que ser desse mesmo tipo.
Os tipos são:
### Númericos
- Inteiros: os tipos inteiros são TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT sendo completamente ligados ao tamanho do valor em bytes, ou seja, o tamanho do número que poderá guardar nesse campo. A propriedade UNSIGNED caracteriza que o campo é unsigned.
- Decimais: temos o tipo de ponto flutuante que fazem um arredondamento em relação a quantidade de casas decimais, podendo ser o FLOAT e o DOUBLE, onde o double tem um arredondamento mais preciso. O outro tipo são os fixos, podendo ser o DECIMAL ou NUMERIC, que são definidos pelo tamanho de dígitos que o número pode ter, podendo ter até 65 digitos. Esse tipo nao faz o arredondamento.
- Bit: nesse tipo podemos armazenar 0 ou 1, e a quantidade definimos anteriormente. O BIT(1) seria 0 ou 1, O BIT(2), seria 00, 01, 10, 11, e assim por diante.
Os atributos para campos númericos são:
- SIGNED ou UNSIGNED: define se vai possui ou não sinal no número;
- ZEROFILL: preenche com zeros os espaços.
- AUTO_INCREMENT: um campo númerico que não é incluído dados, onde o banco sozinho que trabalha nesse campo, que aumenta de 1 em 1 em relação à cada valor que colocamos, ou incrementa em uma quantidade que definirmos.
- OUT OF RANGE: são erros que ocorrem quando os valoers estouram os limites.

### Data e Hora
- DATE: 1000-01-01 até 9999-12-31;
- DATETIME: 1000-01-01 00:00:00 até 9999-12-31 23:59:59;
- TIMESTAMP: range menor que o DATETIME e imprime o fuso-horário. 1970-01-01 00:00:01 UTC até 203-01-19 UTC;
- TIME: -838:59:59 à 839:59:59;
- YEAR: pode armazenar 2 ou 4 dígitos, 1901 à 2155.

### String
- CHAR: cadeia de caracteres com valor fixo, de 0 à 255.
- VARCHAR: cadeia de caracteres com valor variado, de 0 à 255.
CHAR(4) "aa" = "  aa" - grava os vazios também, gasta mais memória.<br>
VARCHAR(4) "aa" = "aa" - não grava os vazios, gasta menos memória.
- BINARY: cadeia de caracteres com valor fixo, de 0 à 255, expressos em binários, e armazena o espaço vazio.
- VARBINARY: cadeia de caracteres com valor fixo, de 0 à 255, expressos em binários, e não armazena o espaço vazio.
- BLOB: binário longo, podendo ser TINYBLOB, BLOB, MEDIUMBLOB, LONGBLOB.
- TEXT: texto longo, podendo ser TINYTEXT, TEXT, MEDIUMTEXT, LONGTEXT
- ENUM: permite armazenar uma lista pré-definida de valores, ou seja, opções.
Alguns atributos importantes para esse tipo são o SET e o COLLATE, que define o tipo de conjunto de caracteres serão suportados, como russo, inglês, japonês, chinês, ou seja, controla a tabela ASC que será utilizada

### Spacial
- GEOMETRY: representa área dentro de um mapa;
- POINT: ponto de latidude e longitude;
- LiNESTRING: representa uma linha dentro de um mapa;
- POLYGON: representa área dentro de um mapa;

<br>

Para criar tabela utilizamos o comando `CREATE TABLE`. Existem boas práticas para criar todos os itens da tabela. Para criar os campos fazendo tudo dentro de um parentêsis definindo o nome e o tipo do campo.
```
CREATE TABLE tbCliente(
CPF VARCHAR(11),
NOME VARCHAR(100),
ENDERECO1 VARCHAR(150),
ENDERECO2 VARCHAR(150),
BAIRRO VARCHAR(50),
CIDADE VARCHAR(50),
ESTADO VARCHAR(50),
CEP VARCHAR(8),
IDADE SMALLINT,
SEXO VARCHAR(1),
LIMITE_CREDITO FLOAT,
VOLUME_COMPRA FLOAT,
PRIMEIRA_COMPRA BIT
);
```
```
CREATE TABLE TABELA_DE_VENDEDORES(
MATRICULA VARCHAR(5),
NOME VARCHAR(100),
PERCENTUAL_COMISSAO FLOAT
);
```
Caso você ja tiver selecionado com o duplo clique o banco, não precisa colocar o nome do banco antes do nome da tabela. Podemos também colocar se o campo irá aceitar null.
```
CREATE TABLE `sucos`.`produtos` (
  `PRODUTO` VARCHAR(20) NULL,
  `NOME` VARCHAR(150) NULL,
  `EMBALAGEM` VARCHAR(50) NULL,
  `TAMANHO` VARCHAR(50) NULL,
  `SABOR` VARCHAR(50) NULL,
  `PRECO_DE_LISTA` FLOAT NULL);
```
Para apagar a tabela podemos utilizar o comando  ou o assistente, clicando com o botão direito na tabela e clicando em `Drop Table`.
```
DROP TABLE tbcliente3;
```

### Inserir um registro
O comando para inserir dados em um banco de dados é o `INSERT` seguido de `INTO` e o nome da tabela. Abrimos os parêntesis e colocamos os nomes dos campos da tabela na ordem que eu receberá a ordem dos dados recebidos. Depois de colocarmos os nomes, utilizamos o comando `VALUES`, abrimos os parêntesis e colocamos os nomes dos campos que cada campo da tabela irá receber.
```
INSERT INTO produtos (
PRODUTO, NOME, EMBALAGEM, TAMANHO, SABOR, PRECO_DE_LISTA) VALUES (
'1040107', 'Light - 350 ml - Melancia', 'Lata', '350ml', 'Melancia', 4.56);
```
Para mostrar essa linha que adicionamos, podemos mostrar a tabela:
```
SELECT * FROM produtos;
```
Para inserir varios produtos de uma vez podemos fazer da seguinte maneira:
```
INSERT INTO produtos (
PRODUTO, NOME, EMBALAGEM, TAMANHO, SABOR, PRECO_DE_LISTA) VALUES (
'1037797', 'Clean - 2 Litros - Laranja', 'PET', '2 Litros', 'Laranja', 16.01);

INSERT INTO produtos (
PRODUTO, NOME, EMBALAGEM, TAMANHO, SABOR, PRECO_DE_LISTA) VALUES (
'100089', 'Sabor da Montanha - 700ml - Uva', 'Garrafa', '700ml', 'Uva', 6.31);

INSERT INTO produtos (
PRODUTO, NOME, EMBALAGEM, TAMANHO, SABOR, PRECO_DE_LISTA) VALUES (
'1004327', 'Videira do Campo - 1,5 Litros - Melância', 'PET', '1,5 Litros', 'Melância', 19.51);
```
Podemos também fazer da seguinte maneira, deixando os valores na mesma linha.
```
INSERT INTO tabela_de_vendedores (
MATRICULA, NOME, PERCENTUAL_COMISSAO) VALUES (
'00235', 'Márcio Almeida Silva', 0.8);

INSERT INTO tabela_de_vendedores (
MATRICULA, NOME, PERCENTUAL_COMISSAO) VALUES (
'00236', 'Cláudia Morais', 0.8);
```
<br>

### Alterar um registro
Para alterar uma informação na tabela utilizamos o comando `UPDATE`, seguido do nome da tabela e do comando `SET`, seguido do campo = novo valor, e seguido do comando `WHERE`, que fará um filtro para o campo que será feito o update.
```
UPDATE produto SET EMBALAGEM = 'Lata', PRECO_LISTA = 2.46
WHERE PRODUTO = "544931";
```

### Excluir um registro
Para excluir registros utilizamos o comando `DELETE FROM` seguido do nome da tabela e do `WHERE`, com o filtro do que será excluído.

### Tornar um campo como chave primária
A chave primária é um campo aonde os registros não podem repetir esse valor. Para isso usamos o comando `ALTER TABLE`, seguido do nome da tabela, seguido do comando `ADD PRIMARY KEY` e o campo entre parentêsis.
```
ALTER TABLE produtos ADD PRIMARY KEY (produto);
```
O ideal é já criar a tabela definindo a chave primária.

### Adicionar um novo campo na tabela
Para criar um campo novo utilizamos o comando `ALTER TABLE`, seguido do nome da tabela, seguido do comando `ADD COLUMN` e entre parêntesis o nome do campo e o seu tipo.
```
ALTER TABLE tbcliente ADD COLUMN (DATA_NASCIMENTO DATE);
```

### Trabalhar com datas
Para inserirmos um valor do tipo data existe um padrão, ela tem que estar entre aspas simples, aí temos YYYY-MM-DD.
```
INSERT INTO tbcliente (
CPF, NOME, ENDERECO1, ENDERECO2, BAIRRO, CIDADE, ESTADO, CEP, IDADE, SEXO, LIMITE_CREDITO, VOLUME_COMPRA,PRIMEIRA_COMPRA,DATA_NASCIMENTO) VALUES(
'00388934505','João da Silva','Rua Projetada A, 10','','Vila Roman','Caratinga','Amazonas','2222222',30,'M', 10000.00,2000,0,'1989-10-05');
```

### Consultando os dados
Podemos limitar a quantidade de registros que sai no select, assim como selecionar quais campos queremos que seja mostrado, utilizando o comando `LIMIT`.
```
SELECT CPF, NOME FROM tbcliente LIMIT 5;
```
Podemos também mudar o nome de cada campo que será exibido, chamado de alias, utilizando o comando `AS`
```
SELECT CPF AS CPF_CLIENTE, NOME AS NOME_CLIENTE FROM tbcliente;
```

### Filtrando Registros
Podemos utilizar o WHERE no SELECT, mostrando apenas algo referente algum filtro, podendo mostrar um ou mais registros, dependendo do filtro.
```
SELECT * FROM tbproduto WHERE PRODUTO = '544931';
```
```
SELECT * FROM tbcliente WHERE CIDADE = 'Rio de Janeiro';
```
Podemos também utilizar o WHERE no UPDATE.
```
UPDATE tbproduto SET SABOR = 'Cítricos' WHERE SABOR = 'Limão';
```
Podemos também usar filtros de maiores, menores e diferentes:
```
SELECT * FROM tbcliente WHERE IDADE > 22;
SELECT * FROM tbcliente WHERE IDADE >= 22;

SELECT * FROM tbcliente WHERE IDADE < 22;
SELECT * FROM tbcliente WHERE IDADE <= 22;

SELECT * FROM tbcliente WHERE IDADE <> 22;
```
Podemos também utilizar esse tipo de filtro para textos.
```
SELECT * FROM tbcliente WHERE NOME > 'F';
```
Com relação aos números de ponto flutuante é mais díficil utilizar condições utilizando o igual ou diferente, pela falta de precisão, sendo um pouco mais fácil para usar com maior ou menor, mas ainda sim é imprecisso. Se quiséssemos mais precisão precisaríamos utilizar o tipo DECIMAL. Outra maneira é utilizar o método `BETWEEN` e `AND` para selecionar limites superiores e inferiores bem próximo do que queremos.
```
SELECT * FROM tbproduto WHERE PRECO_LISTA BETWEEN 16.007 AND 16.009;
```

Para fitrar datas podemos utilizar os mesmos operadores com o WHERE.
```
SELECT * FROM tbcliente WHERE DATA_NASCIMENTO = '1995-01-13';

SELECT * FROM tbcliente WHERE DATA_NASCIMENTO > '1995-01-13';
SELECT * FROM tbcliente WHERE DATA_NASCIMENTO >= '1995-01-13';

SELECT * FROM tbcliente WHERE DATA_NASCIMENTO < '1995-01-13';
SELECT * FROM tbcliente WHERE DATA_NASCIMENTO <= '1995-01-13';

SELECT * FROM tbcliente WHERE DATA_NASCIMENTO <> '1995-01-13';
```
Podemos também utilizar algumas funções:
```
SELECT * FROM tbcliente WHERE YEAR(DATA_NASCIMENTO) = '1995';

SELECT * FROM tbcliente WHERE month(DATA_NASCIMENTO) = '10';
```

Podemos também utilizar filtros compostos, com o comando `AND` e o comando `OR`:
```
SELECT * FROM tbproduto WHERE PRECO_LISTA >= 16.007 AND PRECO_LISTA<=16.009;

SELECT * FROM tbcliente WHERE IDADE>= 18 AND IDADE<=22 AND SEXO = 'M';
```
```
SELECT * FROM tbcliente WHERE CIDADE = 'Rio de Janeiro' OR BAIRRO = 'Jardins';
```
```
SELECT * FROM tbcliente WHERE (IDADE>=18 AND IDADE <=22 AND SEXO='M') OR (CIDADE = 'Rio de Janeiro' OR BAIRRO = 'Jardins');
```
Os comandos `AND` e `OR` também podem ser utilizados nos comandos UPDATE e DELETE.