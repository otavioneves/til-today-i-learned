A linguagem "SQL" não é uma linguagem estruturada. Ela não possui, por exemplo, comando de repetição, "IF" "THE", "ELSE". Geralmente, é uma sequência de comandos, onde eu posso colocar "SELECTS", "INSERTS", "UPDATES", "DELETES", "CREATE", "DROP, e assim por diante.<br>
Para resolver essa deficiência na linguagem SQL foi criada uma linguagem interna estruturada de cada banco de dados. Essa linguagem interna possuí comandos, loops, etc.<br>
Dentro do MySQL a linguagem interna é a Stored Procedures. Podemos criar procedures utilizando o comando `CREATE PROCEDURE` com a seguinte estrutura:
```
CREATE PROCEDURE

procedure_name(parameters)

BEGIN

DECLARE declaration_statement;
...
executable_statement;
...
END;
```
- O nome de uma Stored Procedure deve ter apenas letras, números, $ e underscore;
- O nome pode ter no máximo 64 caracteres;
- O nome deve ser único dentro do banco;
- É case sensitive.

Podemos criar uma Stored Procedure simples. Para criar clicamos no ícone das Stored Procedure e depois em Create:
```
CREATE PROCEDURE `HelloWorld` ()
BEGIN
	SELECT 'Hello World!';
END
```
Para chamar uma Stored Procedure utilizar o comando `CALL`.
```
CALL HelloWorld;
```
Podemos utilizar os alias para dar um nome as colunas criadas.
```
CREATE DEFINER=`root`@`localhost` PROCEDURE `MostraNumeroComAlias`()
BEGIN
	SELECT (1+9) - 5 AS RESULTADO;
END
```
Podemos também fazer comentários nos Stored Procedure.
```
CREATE PROCEDURE `SPComComentários` ()
BEGIN
	/*Vamos exibir itens combinados entre textos e números */
    -- Usando a função CONCAT. O traço traço serve para quando o comentário é apenas em uma linha.
	SELECT CONCAT('Hello World! ', (1+9)-5) as ITENS_COMBINADOS;
END
```
Para alterar podemos clicar em cima da que iremos alterar e depois em Alter Stored Procedure.<br>
Par apagar, clicamos sobre ela é clicamos em Drop Stored Procedure.<br>

Podemos criar varíavel através do comando `DECLARE` com a seguinte sintaxe:
```
DECLARE variable_name datatype DEFAULT value;
```
- O nome da varíavel deve ter apenas letras, números, $ e underscore;
- O nome pode ter no máximo 255 caracteres;
- O nome deve ser único dentro da Stored Procedure;
- É case sensitive.
- Se não houver DEFAULT o valor da varíavel será NULL;
- A linha da declaração deve terminar com ponto e vírgula.
Alguns tipos de varíaveis são:
- VARCHAR(número de digitos);
- INTEGER;
- DECIMAL(número de digitos, número de casas decimais);
- DATE;
- TIMESTAMP.
```
CREATE PROCEDURE `ExibeVariavel` ()
BEGIN
	DECLARE TEXTO VARCHAR(12) DEFAULT 'Hello World!';
	
    SELECT TEXTO;
END
```
O objetivo de uma Stored Procedures é manipular o banco de dados.<br>
Uma Stored Procedure pode também receber parâmetros.<br>
Podemos fazer um tratamento de erro através do comando `DECLARE EXIT HANDLER FOR`, com a seguinte síntaxe, e que só será executado caso aconteça o erro definido.
```
DECLARE EXIT HANDLER FOR númerodoerro
BEGIN
    comando
END
```
Para declarar uma varíavel utilizamos o comando SET.<br>
Para que a varíavel receba um campo do registro do banco, a varíavel receberá o resultado de um SELECT e com o comando INTO.
```
SELECT sabor INTO vSabor FROM tabela_de_Produtos WHERE codigo_do_produto = vProduto;
```

### Controle de Fluxo IF
```
IF condition THEN
    comandos;
ELSE
    comandos;
END IF
```
```
IF condition THEN
    comandos;
ELSE IF
    comandos;
ELSE IF
    comandos;
ELSE IF
    comandos;
END IF
```

### Controle de fluxo CASE
```
CASE varíavel
WHEN valor1 THEN comando1;
WHEN valor2 THEN comando2;
WHEN ...;
ELSE comandocasonãotenhanenhumvalor
END CASE;
```
Para proteger o CASE, para casos de valor não encontrado, podemos utilizar o tratador de erros `DECLARE CONTINUE HANDLER FOR 1339 SET mensagemdeerro = 'mensagem de erro'`.<br>
Podemos colocar também para o CASE verificar condições, e não somente valores.

### Controle de fluxo WHILE
```
WHILE condição
DO
    comandos;
END WHILE;
```

### CURSOR
O cursos é uma varíavel como se fosse um array, que pode receber um select, e pode ser trabalhado através de um looping. O Cursor é uma estrutura implementada no MySQL que permite uma interatividade linha a linha de uma determinada ordem. O cursos é declarado, aberto para percorrrer linha a linha, percorre linha a linha até o final, fecha o Cursos e limpa o Cursos da memória.
```
DECLARE cursor1 CURSOR FOR SELECT nome FROM tabela;

OPEN CURSOR1;
FETCH CURSOR1 INTO @NOME;
FETCH CURSOR1 INTO @NOME;
FETCH CURSOR1 INTO @NOME;
FETCH CURSOR1 INTO @NOME;

CLORE CURSOR;
```

### Função
A função diferente da Stored Procedure, que recebe uma série de comandos sem retornar nada, retorna algo para ser usada em alguma outra função, Stored Procedure, ou mesmo um comando.
```
CREATE FUNCTION nome (parâmetros)
RETURNS tipoderetorno
BEGIN

DECLARE varíaveis;

comandos;

RETURN comandos;

END;
```
Para o MySQL poder criar funções precisamos declarar o seguinte parâmetro.
```
SET GLOBAL log_bin_trust_function_creators = 1;
```