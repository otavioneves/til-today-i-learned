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