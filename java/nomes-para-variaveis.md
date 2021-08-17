Uma boa prática de desenvolvimento é colocar bons nomes que deixam minimamente descrito a função de cada varíavel no próprio nome, o que facilita a revisão e trabalho em equipe.<br>
Para começar, o Java aceita como nome de varíavel os nomes com as seguintes regras:
- Pode começar com qualquer letra, $ ou -;
- Pode conter números mas não pode começar com números;
- Não pode conter caracteres especiais @ ! % &;
- Não é recomendado utilizar acentos.
Exemplo:
```
Double valorProduto = 100.0; // Melhor
Double valorproduto = 100.0; // Mais dificil para ver a separação de palavras
Double vlrPrd = 100.0; // Podemos confundir o que realmente significa
Double vlrprd = 100.0; // Confusão e dificuldade de separar abreviações
Double vp = 100.0; // Bem ruim
Double x = 100.0; // Péssimo
```