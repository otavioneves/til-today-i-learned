As camadas de uma aplicação utilizando JDBC, DAO, Banco de Dados, é:
- View: visualização, aonde o usuário insere dados, altera, exclui, etc, ou seja, interaje com os dados. Essa camada não atua diretamente no Banco de Dados.
- Controller: controlador, camada que pega as interações feitas pelo usuário na camada de visualização e interaje com o DAO, que faz a comunicação com o Banco de Dados.
- DAO: a camada DAO faz a comunicação com o Banco de Dados.
- Modelo: camada de modelo.
