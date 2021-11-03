O backup é uma cópia feita periodicamente para possível recuperação futura. Existem dois tipos de backup, o lógico e o físico. O lógico é mais lento, são comandos dentro de um script. O físico é mais rápido.<br>
Para fazer backups lógicos utilizamos o mysqldump.
```
mysqldump -uroot -p --databases sucos_vendas > c:/mysqladmin\sucos_vendas_full.sql
```
Podemos também fazer o backup com Dump através do Data Export no Worbench.<br>
Para fazer os backups o ideal é trancar o banco de dados à alterações, utilizando o comando `LOCK INSTANCE FOR BACKUP`. Para desbloquear utilizamos `UNLOCK INSTANCE`.<br>
Uma boa prática é fazer os dois tipos de backup, o lógico e o físico.