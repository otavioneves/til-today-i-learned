Para trabalhar com algum banco de dados precisamos ir em Schema e clicar em cima do banco de dados que queremos trabalhar, ou usar o comando `USE nomedobanco`. Podemos com isso rodar comandos.<br>
Podemos digitar mais de um comando.
```
SELECT * FROM CITY;

SELECT * FROM COUNTRY;
```
Selecionando apenas uma das linhas, podemos executar apenas essa linha, enquanto a outro não.<br>
O WorkBench mostra os erros antes de rodas quando o erro é algo relacionado aos comandos, ao sistema. Erros por exemplo de digitação do nome do banco, dará erro em tempo de execução.<br>
Para criar um banco de dados utilizamos o comando `CREATE DATABASE`, que pode receber uma condição IF NOT EXISTS, para verificar se o banco ja existe. Podemos também crira a especificação do banco, como:
- CHARACTER SET: é o charset que define com qual conjunto de caracteres utilizaremos, como acentos, etc;
- COLLATE: especifica o padrão do charset;
- DEFAULT ENCRYPTION: especifica se terá encriptação ou não.
```
CREATE DATABASE `SUCOS` DEFAULT CHARACTER SER UTF8;
```
Podemos também criar um banco de dados utilizando um assistente do WorkBench.<br>
Para apagar o banco de dados utilizamos o comando `DROP DATABASE`. Podemos também ir com o botão direito do mouse e clicar em Drop Schema.
```
DROP DATABASE `SUCOS`;
```