O auto incremento é um número que vai sendo incrementado a cada insert na tabela. Ao criar uma tabela, o campo de autoincremento sempre deve ser chave primária;
```
CREATE TABLE tab_identity (
ID INT AUTO_INCREMENT,
DESCRITOR VARCHAR(20),
PRIMARY KEY (ID));

INSERT INTO TAB_IDENTITY (DESCRITOR) VALUES ('CLIENTE1');
INSERT INTO TAB_IDENTITY (DESCRITOR) VALUES ('CLIENTE2');
INSERT INTO TAB_IDENTITY (DESCRITOR) VALUES ('CLIENTE3');

SELECT * FROM tab_identity;
```
Caso algum registro venha a ser excluído, o ID vai com ele, e o próximo registro à ser inserido terá um ID que continuará a sequência.<br>
Podemos também forçar o ID, mas a partir do momento que forçamos esse novo ID, a sequência continuará do número colocado.