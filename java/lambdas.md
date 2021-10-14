A alternativa que vem para simplificar as classes anônimas são os Lambdas. Nos lambdas nós trocamos um método que seria definido dentro de uma classe, a qual teríamos que instanciar um objeto para poder implementar seus métodos, por um chamamento semelhante ao das classes anônimas, porém mais simplicado.<br>
Nesse caso, declaramos da seguinte maneira:
- Parâmetros que o método receberia;
- O sinal ->;
- Abre chaves e implementa o método.
```
lista.sort((Conta c1, Conta c2) -> {
                return Integer.compare(c1.getNumero(), c2.getNumero());
            }
);
```
Outro exemplo:
```
Comparator<Conta> comp = (Conta c1, Conta c2) {
                            String nomeC1 = c1.getTitular().getNome();
                            String nomeC2 = c2.getTitular().getNome();
                            return nomeC1.compareTo(nomeC2);
                };
```
Podemos também enxugar mais ainda, no caso de códigos com uma linha:
- Parâmetros que o método receberia;
- O sinal ->;
- Implementa o método.
```
lista.sort( (c1, c2) -> Integer.compare(c1.getNumero(), c2.getNumero()) );
```
Um outro exemplo é o seguinte, chamar o método foreach da List, já implementando o que queremos em cada loop:
```
lista.forEach( (Conta conta) -> System.out.println(conta + ", " + conta.getTitular().getNome()));

// Leitura: para essa lista, faça um forEach para cada elemento que for uma Conta, imprimindo esses elementos
```