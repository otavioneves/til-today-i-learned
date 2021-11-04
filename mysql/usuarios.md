Para configurar usuários podemos ir em Administration e Users and Privileges.<br>
Podemos colocar o nome do usuário, o host, a senha. Na segunda aba, podemos colocar limites de consultas, updates, connection, etc. Na terceira aba configuramos os privilégios que o usuário terá, ou seja, os comandos que ele poderá utilizar.<br>
O ideal é criar logins de administrador, usuário comum (que terá os seguintes privilégios: SELECT, INSERT, UPDATE, DELETE, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE), um usuário somente para leitura e um usuário que só pode fazer backup (SELECT, RELOAD, LOCK TABLES, REPLICATION CLIENT).<br>
Podemos também definir qual é o range de máquinas que cada usuário pode usar para se conectar com a base.<br>

### Exemplo:

Para um banco chamado BANCODB, com as seguintes tabelas:
- TABELA1
- TABELA2
- TABELA3
Para dar acesso apenas à leitura das tabelas TABELA1 e TABELA2, e acesso completo à TABELA3. Sabendo que já temos um usuário user@% criado, os comandos SQL para configurar este acesso são:
```
GRANT SELECT, INSERT, UPDATE, DELETE, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE 
ON BANCODB .TABELA3 TO 'user'@'%';

GRANT SELECT, EXECUTE 
ON BANCODB .TABELA1 TO 'user'@'%';

GRANT SELECT, EXECUTE 
ON BANCODB .TABELA2 TO 'user'@'%';
```

Podemos também revogar previlégios de duas maneiras, utilizando o Adminstration ou na linha de comando, utilizando o comando `REVOKE ALL PRIVILEGES, GRANT OPTION FROM usuário;`.