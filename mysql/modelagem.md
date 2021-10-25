Para projetar um banco de dados precisamos dos seguintes requisitos:
- Entendimento das regras de negócio;
- Efetuar atividades de entrevistas e reuniões;
- Desenho de modelo mais fiel à realidade.
Após ter levantado essas informação temos um modelo conceitual, construindo um diagrama de Entidade e Relacionamento, estabalecendo uma cardinalidade entre as entidades. Exemplo:
- "Um VENDEDOR realiza uma VENDA, um CLIENTE está contido em uma VENDA, a VENDA possuí ITENS_VENDIDOS, e os ITENS_VENDIDOS possuem PRODUTOS".
- "1 vendedor pode estar realionado à N VENDAS, assim com o cliente. Já a VENDA é sempre única, e possui N ITENS_VENDIDOS. Cada ITENS_VENDIDOS possuí 1 PRODUTOS".
<br>
Após isso, estabelecemos as características de cada entidade, aonde cada tabela recebe as informações dos campos, tipos, etc. Os diagramas viram então tabelas, onde definimos chaves primárias e os relacionamentos com as chaves estrangeiras.<br>
Para construir através das ferramentas CASE, aonde desenhamos de maneira gráfica as tabelas e a ferramenta cria a tabela. Podemos também fazer pelo workbench, sem nenhum problema.