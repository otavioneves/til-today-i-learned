Para fazer o deploy no Heroku, criamos um novo projeto no site do Heroku, aonde utilizaremos o Heroku CLI.<br>
Adicionamos em Resources, o banco de dados.<br>
Na aplicação, é necessário retirar os dados referentes aos ambientes de testes, principalmente a informação do localhost:8080, pois não será nessa url que a aplicação irá rodar. Para configurar a aplicação, criamos uma cópia do application.properties com o nome application-prod.properties. Nesse novo arquivo colocaremos as seguintes informações:

```
#MYYSQL                mysql://    [username]:[password]@[host]/[database]         
spring.datasource.url= mysql://b3971ea5533bef:a71805b6@us-cdbr-east-05.cleardb.net/heroku_70be3875cc7edba?reconnect=true

spring.jpa.hibernate.ddl-auto= update
spring.jpa.show-sql= false
spring.jpa.open-in-view= true

spring.thymeleaf.cache= true
```

Criamos também um arquivo na raiz do projeto com o nome Procfile, sem extensão nenhuma.
```
web: java -Dserver.port=$PORT -Dspring.profiles.active=prod -jar target/demo-0.0.1-SNAPSHOT.jar
```
Iniciamos esse repositório no git e seguimos as orientações do Heroku.<br>
A aplicação ficará na nuvem do Heroku. Para ver os logs podemos rodar o comando `heroku logs --tail`.<br>
Para fazer o deploy, rodamos o comando `heroku open`.<br>
Para verificar as informações do banco podemos abrir o workbench e criar uma nova conexão, utilizando os dados de username, host, password e nome do database