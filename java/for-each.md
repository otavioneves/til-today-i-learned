O for each é um for melhorado é muito utilizado com Arrays. O for each possui um contador interno, não sendo necessário utilizar o contador dentro do laço, conforme exemplificado abaixo a maneira do for normal:
```
Notas[] notas = new Notas[10];

for (int i=0; i<notas.length;i++){
    System.out.println(notas[i])
}
```
O `for each` ficaria da seguinte maneira: Criamos uma variavel int que recebe o array e pedimos para escrever apenas essa varíavel. A cada loop será feito exatamente como acima.
```
Notas[] notas = new Notas[10];

for (int nota : notas){             // o int é o tipo do Array, a varíavel é o nome do Array no singular
    System.out.println(nota)        // imprimimos a variavel int nota
}
```
Devido ao conceito de referência e valor, na hora de settar os valores nos arrays não da pra usar o for each, sendo recomendado para o output.<br>
For normal para settar, for each para output.