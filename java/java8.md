Com o lançamento do Java 8 tivemos várias novidades, algumas delas formam um tripé: os Default Methods, os Lambdas e os Method References.
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
Esse método foi criado com o modificador default, que faz com que sistemas que já estavam rodando não quebrem com a nova implementação.<br>
Podemos também, após no Java 8 terem sido criados diversos métodos estáticos para o java.util, utilizar o método comparing em um comparator, dentro do método sort, que recebe uma Function, ou um Lambda.
```
// maneira comum e mais adequada:

palavras.sort(Comparator.comparing(s -> s.length()));     

// palavras ordene comparando o tamanho da String

// o lambda recebe o tamanho de uma string, que é passado para o comparing, o método comparing vai criar um Comparator que dada cada uma das String, ele pega o tamanho dela e compara entre duas, virando uma factory de comparators. Isso é passado para o método sort, que compara elas.
```
Isso é o mesmo que:
```
Comparator<String> comparador = Comparator.comparing(s -> s.length());
palavras.sort(comparador);
```
Da maneira mais detalhada temos:
```
Function<String, Integer> funcao = s -> s.length();             // dado uma string, devolveremos um Integer (tamanho da String)
Comparator<String> comparador = Comparator.comparing(funcao);           // recebendo a função como argumento pra criar um Comparator
palavras.sort(comparador);          // faz o sort
```
A interface Function vai nos ajudar a passar um objeto para o Comparator.comparing que diz qual será a informação que queremos usar como critério de comparação. Ela recebe dois tipos genéricos. No nosso caso, recebe uma String, que é o tipo que queremos comparar, e um Integer, que é o que queremos extrair dessa string para usar como critério. <br>

Pode ainda ficar mais simples, que é um método Reference, que substitui um método bem simples:
`String:lenght`
```
palavras.sort(Comparator.comparing(String::lenght);     
```
O método Reference é um lambda de uma maneira mais enxuta, tanto que é igual as duas linhas:
```
Function<String, Integer> funcao = String::length;
Function<String, Integer> funcao = s -> s.length();
```
Também serve para outros métodos:
```
Consumer<String> impressor = System.out:println;
palavras.forEach(impressor);
```

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
EXEMPLO COMPLETO:
```
List<Curso> cursos = new ArrayList<Curso>();
cursos.add(new Curso("Python", 45));
cursos.add(new Curso("JavaScript", 150));
cursos.add(new Curso("Java 8", 113));
cursos.add(new Curso("C", 55));
		
cursos.sort(Comparator.comparingInt(Curso::getAlunos));		// ordenando
		
cursos.forEach(System.out::println);		// iterando imprindo pelo to String
		
cursos.forEach(c -> System.out.println(c.getNome()));		// iterando imprimindo o nome
		
System.out.println(cursos);		// imprimindo o to string da List
```
Além desse tripé, temos as novidades referente ao Stream, aonde toda Collection agora tem esse método Stream(), que retorna um fluxo de objetos. A partir desse método podemos chamar vários métodos estáticos. O método Stream não impacta a collection original diretamente, devemos por isso trabalhar dentro desse Stream.
- filter: filtra por alguma condição:
```
cursos.stream().filter(c -> c.getAlunos() >= 100).forEach(System.out::println);

// a List cursos chama o método stream, que chama o método filter que recebe uma condição para filtragem, e logo após chamamos o método forEach, que irá iterar imprimindo aquilo que foi filtrado. A collection original não é alterada.
```
- map: dado um Stream de Cursos, podemos transformar em um stream de alguma outra coisa, através do método map.
```
cursos.stream().filter(c -> c.getAlunos() >= 100).map(c -> c.getAlunos()).forEach(total -> System.out.println(total));

// a List cursos chama o método stream, que chama o método filter que recebe uma condição para filtragem, e logo após chamamos o método map, que irá transformar em uma Stream de Integers, e após isso chamamos um forEach para imprimir essa Stream.
```
O método mapToInt transforma em um IntStream, que por ser um Stream de Integers tem vários métodos para trabalhar com Integers.
```
int sum = cursos.stream().filter(c -> c.getAlunos() >= 100).mapToInt(c -> c.getAlunos()).sum();
System.out.println(sum);

// cursos transforma em um Stream, que é filtrado, o map transforma em um Stream de int que possui o método sum, entre muitos outros, que soma o que for passado.
```
Para escolhermos um dentro de um filtro podemos usar o método `findAny` ou `findFirst`, aonde poderíamos passar mais algumas condições para esse find.<br>
A classe Optional é utilizada quando trabalhamos com possibilidades de null, evitando aqueles `if=null...`. Essa Classe tem algumas métodos, como o get, que caso tenha encontrado ele retorna o que encontrou, caso não ele lança uma exception.
```
Optional<Curso> optionalCurso = cursos.stream().filter(c -> c.getAlunos()>=100).findAny();
		
System.out.println(optionalCurso.get());
		
// podemos também transformar esse Optional em um Curso em si, utilizando o método orElse: devolva, se não, devolva null
		
Curso curso = optionalCurso.orElse(null);
		
System.out.println(curso.getNome());

// podemos também utilizar o ifPresent, que recebe um lambda, nesse caso onde escrevemos: caso tenha algum curso, imprima, caso não, não faça nada.
		
optionalCurso.ifPresent(c -> System.out.println(c.getNome()));
		
// podemos fazer também da seguinte maneira:
		
cursos.stream().filter(c -> c.getAlunos()>=100).findAny().ifPresent(c -> System.out.println(c.getNome()));
		
// outro método que podemos utilizar é o average, que calcula a media
		
OptionalDouble media = cursos.stream().filter(c -> c.getAlunos() >= 100).mapToInt(c -> c.getAlunos()).average();

// o método collect é utilizado para coletar e guardar dentro de um Collector, que é uma classe que possuí varios métodos que transformarão em uma Collection, como list, map, set. Essa maneira faz com que possamos filtrar e jogar novamente na Collection original, saindo do Stream.
		
cursos = cursos.stream().filter(c -> c.getAlunos()>=100).collect(Collectors.toList());
		
System.out.println(cursos);
		
```
- Outra novidade do java 8 foi a classe para tratar com datas.