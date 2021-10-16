A API do Java chamada ArrayList é uma estrutura de dados pronta que tem muitas funcionalidades já prontas. Essa Classe pertence ao pacote java.util, assim como a maioria das Collections (as estruturas de dados prontas do Java).<br>
O ArrayList é um vetor que podemos passar o tipo que ele será, utilizando os Generics.<br>
Essa classe cresce conforme necessitamos, sendo muito útil.
```
ArrayList<String> arrayList = new ArrayList<String>();          // no momento de instanciar podemos já passar os elementos iniciais que queremos, podemos instanciar sem nada, e podemos passar uma capacidade inicial.
```
Para adicionar um elemento podemos utilizar o método add, que adiciona o elemento passado e retorna um booleando informando se o elemento foi adicionado com sucesso ou não.
```
arrayList.add("A");
```
Para imprimirmos o array podemos simplemente chamar o nome dele, que automaticamente chama o .toString.
```
System.out.println(arrayList);
```
Para adicionar um elemento em uma posição específica, podemos adicionar passando a posição e o elemento:
```
arrayList.add(1, "B");
```
Para executarmos uma busca por um elemento, podemos utilizar o método `.contains`, que retorna um boolean:
```
boolean existe = arrayList.contains("A");

if (existe){
	System.out.println("Elemento existe no array");
} else {
	System.out.println("Elemento não existe no array");
}
```
Para executarmos uma busca por um elemento, podemos utilizar também o método `.indexOd`, que retorna a posição do elemento no vetor, caso ele não encontre, retorna -1: 
```
int pos = arrayList.indexOf("B");

if (pos > -1){                 // verificação para caso não encontre o elemento no vetor
	System.out.println("Elemento existe no array na pos " + pos);
} else {
	System.out.println("Elemento não existe no array " + pos);
}
```
Para mostrarmos o elemento em certa posição, podemos usar o método `.get`, chamado também de busca por posição, que retorna o elemento da posição passada. Caso passe uma posição não existente no vetor, dispara uma exception de OutOfBounds.
```
System.out.println(arrayList.get(2));
```
Para remover, utilizamos o método `.remove`, que pode ser passando o índice ou o objeto, nesse último caso
```
arrayList.remove(0);
arrayList.remove("B");
```
Para obtermos o tamanho do array, utilizamos o método `.size`
```
System.out.println(arrayList.size());
```
Uma caracterítica da List é que ela aceita duplicadas, ou seja, adicionar em dois elementos da lista com a mesma referência. Caso queiramos que não tenha duplicados, temos que escrever uma lógica que utiliza o `.contains`. Ela também implementa a interface Collections, além da List. As listas também só guardam referências (String, Classes, Wrappers, etc), não guardam primitivos (como int, double, boolean, etc).<br>
As listas também só guardam referências (String, Classes, Wrappers, etc), não guardam primitivos (como int, double, boolean, etc). Caso queiramos adicionar um item primitivo o java utiliza o Autoboxing, para transformar esse tipo primitivo em uma Referência.
```
String[] nomes = new String[5];

int idade = 29;
Integer idadeRef = new Integer(29);
List<Integer> numeros = new ArrayList<Integer>();

numeros.add(idade);     // inválido, pois idade é um int, tipo primitivo

numeros.add(29);        // válido, estamos adicionando um 29, que seria um int, tipo primitivo, Autoboxing
```
Para fazer um for dentro de uma collection, no caso, um ArrayList, podemos utilizar o método `forEach`, que recebe uma action, que é um Consumer. Podemos colocar como argumento uma expressão lambda.
```
String aula1 = "Modelando a classe Aula";
String aula2 = "Conhecendo mais de listas";
String aula3 = "Trabalhando com Cursos e Sets";

ArrayList<String> aulas = new ArrayList<>();
aulas.add(aula1);
aulas.add(aula2);
aulas.add(aula3);

aulas.forEach(aula -> {
    System.out.println("Percorrendo:");
    System.out.println("Aula " + aula);
});   
```

A diferença de ArrayList com LinkedList é basicamente performance. O ArrayList, como diz o nome, internamente usa um array para guardar os elementos. Ele consegue fazer operações de maneira muito eficiente, como invocar o método get(indice). Se você precisa pegar o décimo quinto elemento, ele te devolverá isso bem rápido. Quando um ArrayList é lento? Quando você for, por exemplo, inserir um novo elemento na primeira posição. Pois a implementação vai precisar mover todos os elementos que estão no começo da lista para a próxima posição. Se há muitos elementos, isso vai demorar... Em computação, chamamos isso de consumo de tempo linear.<br>
Já o LinkedList possui uma grande vantagem aqui. Ele utiliza a estrutura de dados chamada lista ligada, e é bastante rápido para adicionar e remover elementos na cabeça da lista, isto é, na primeira posição. Mas é lento se você precisar acessar um determinado elemento, pois a implementação precisará percorrer todos os elementos até chegar ao décimo quinto, por exemplo.<br>
O ideal é utilizar a implementação mais genérica, para isso, utilizamos a referência a List, comprometendo-nos pouco, podemos sempre mudar a implementação, isso é, em quem damos new, caso percebamos que é melhor uma ou outra lista nesse caso em particular.<br><br><br>
Um método interessante quando não queremos que alguma lista seja modificada diretamente por um método, colocamos o `.unmodifiableLista(List<>)`, que recebe uma lista, dentro do método e retorna o objeto mas de uma maneira voltada para leitura, não para modificar.
```
public List<Aula> getAulas(){
	return Collections.unmodifiableList(aulas);
}
```
Para poder mexer nesse atributo, temos que fazer uma espécie de uma cópia deixando uma lista imutável e um lista que pode ser mudada.
```
List<Aula> aulasImutaveis = javaColecoes.getAulas();
		
List<Aula> aulas = new ArrayList<>(aulasImutaveis);			// list que pode ser mudada
```
Além do método sort(), a classe Collections também possui muitos outros métodos interessantes:
- Collections.reverse(): O método reverse() serve para inverter a ordem de uma lista. As vezes precisamos imprimir uma lista de nomes do último para o primeiro, ou uma lista de ids do maior para o menor e é nestas horas que utilizamos o reverse para inverter a ordem natural da lista para nós.
- Collections.shuffle(): O método shuffle() serve para embaralhar a ordem de uma lista. Por exemplo em um caso de um sistema de sorteio, em que precisamos de uma ordem aleatória na nossa lista, utilizamos o método shuffle para embaralhá-la.
- Collections.singletonList(): O método singletonList() nos devolve uma lista imutável que contêm um único elemento especificado. Ele é útil quando precisamos passar um único elemento para uma API que só aceita uma Collections daquele elemento.
- Collections.nCopies(): O método nCopies() nos retorna uma lista imutável com a quantidade escolhida de um determinado elemento. Se temos uma lista específica e precisamos obter uma outra lista imutável , contendo diversas cópias de um destes objetos, utilizamos o método nCopies(). O bom deste método é que mesmo que nós solicitemos uma lista com um número grande, como 10000 objetos, ele na verdade se referencia a apenas um, ocupando assim um pequeno espaço. Este método também é utilizado para inicializar Listas recém criadas com Null, já que ele pode rapidamente criar diversos objetos, deste modo:
```
List<Type> list = new ArrayList<Type>(Collections.nCopies(1000, (Type)null));
```
Escolhemos um Set quando não queremos uma lista ordenada e não queremos itens repetidos.<br>
Escolhemos um List quando queremos uma lista ordenado e queremos itens repetidos.<br>
Provavelmente, caso a modelagem do sistema ainda não esteja bem definida, o desenvolvedor irá utilizar a interface Collection. Dessa maneira, terá acesso aos métodos básicos de todas as implementações, como size(), add(), remove() e contains(). Conforme for sentindo necessidade em algo específico, o desenvolvedor fará poucas mudanças em seu código.<br>
Caso sinta necessidade de fazer uma requisição a um elemento específico através da sua posição, trocará de Collection para List. Caso perceba que ordem não importa, porém é necessária uma busca bem rápida (e sem repetições), um Set é mais apropriado.<br>
Enquanto não sentir essa necessidade, provavelmente a Collection será a melhor escolha.