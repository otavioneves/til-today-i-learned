Podemos organizar nossos projetos com os pacotes, que não servem apenas como modo de organização, mas também influencia no funcionamento do código, devido aos modificadores de acesso.<br>
No Java, as classes tem o que chamamos de FQN, ou Full Qualified Name, que é o nome do pacote seguido do nome da classe. É esse FQN que o compilador usa, e não apenas o nome da classe. Para podermos deixar os nomes FQN mais individuais possível, ou seja, para que não exista outra classe FQN com o mesmo nome em outro projeto, utilizamos por convenção a URL da aplicação ou da empresa, seguido do nome do projeto, e seguido das pastas específicas do projeto, sempre separados por pontos.<br>
```
package com.otavio.banco.model
``` 
Para usarmos classes de outros pacotes no nosso projeto, deveriámos sempre usar o FQN, como abaixo:
```
com.otavio.banco.model.ContaCorrente cc = new com.otavio.banco.model.ContaCorrente(1234,4567);
```
Porém, essa é uma forma ruim de fazer isso. A melhor maneira é importando o pacote, não sendo necessário mais usar o FQN para chamar essa outra classe de outro pacote. Usamos o nome FQN, seguido de ponto e o asterisco, que libera todas as classes desse projeto.
```
import com.otavio.banco.model.*
```
No Eclipse, podemos através do atalho CTRL + Shift + O importar todas as classes específicas que estão sendo usadas no código mas ainda não estão importadas. Costumasse utilizar os imports específicos, importando apenas as classes que precisamos utilizar.
```
import com.otavio.banco.model.ContaCorrente;
import com.otavio.banco.model.ContaPoupanca;
import com.otavio.banco.model.CalculadoraImpostos;
```