Com o lançamento do Java 8 tivemos várias novidades, algumas delas são:
- Ordenação de Strings: para ordenar uma list, foi colocada internamente o método sort, que recebe um Comparator:
```
Comparator<String> comparador = new ComparadorDeStringPorTamanho();
palavras.sort(comparador);
```
```
class ComparadorDeStringPorTamanho implements Comparator<String> {
    public int compare(String s1, String s2) {
        if(s1.length() < s2.length()) 
            return -1;
        if(s1.length() > s2.length()) 
            return 1;
        return 0;
    }
}
```
Esse método foi criado com o modificador default, que faz com que sistemas que já estavam rodando não quebrem com a nova implementação.
- Imprimir vários elementos (forEach): o método novo forEach recebe um Consumer. Um consumidor de Strings é uma classe que implementa Consumer, que é caracterizado pelo método accept, que sobreescrevemos esse método na nossa clase.
```
class ConsumidorDeString implements Consumer<String> {
    public void accept(String s) {
        System.out.println(s);
    }
}
```
```
Consumer<String> consumidor = new ConsumidorDeString();
palavras.forEach(consumidor);
```
O método forEach também é um método default. A grande vantagem de um método default é que uma interface pode evoluir sem quebrar compatibilidade.
- Lambdas: A alternativa que vem para simplificar as classes anônimas são os Lambdas. Nos lambdas nós trocamos um método que seria definido dentro de uma classe, a qual teríamos que instanciar um objeto para poder implementar seus métodos, por um chamamento semelhante ao das classes anônimas, porém mais simplicado.<br>
Nesse caso, declaramos da seguinte maneira: Parâmetros que o método receberia; O sinal ->; Abre chaves e implementa o método.
```
palavras.forEach(new Consumer<String>() {
    public void accept(String s) {
        System.out.println(s);
    }
});
```
A nova sintaxe do Java para os lambdas é que quando fica evidente qual o tipo da classe e o método que iremos implementar, não é necessário mais colocá-los.
```
palavras.forEach((String s) -> {
        System.out.println(s);
);
```
Mais ainda, o Java consegue entender antecipadamente que o s será uma String, por isso podemos tirar. E quando é apenas um comando, podemos tirar as chaves.
```
palavras.forEach(s -> System.out.println(s));       // para cada String s, escreva s
```