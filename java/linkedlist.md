Os LinkedLists funciona semelhante ao ArrayList, porém não utiliza um array por baixo dos panos, o que simplifica algumas questões deficientes no ArrayList.<br>
O LinkedList funciona como uma estrutura de dados onde o item tem um ponteiro ao item da frente e ao de trás, criando esses links que geram uma lista duplamente encadeada. Sabemos que estamos no final da lista quando não temos link com um da frente, e sabemos que o inicio da lista é quem não tem link com um de trás.<br>
Com isso, facilitamos para apagar um item no meio, inicio ou fim, e ele se reorganiza.<br>
Uma desvantagem que para chegar no último elemento da lista, temos que começar do começo perguntando à todos os itens quem são o seu próximo, ou seja, não é eficiente para iterar.<br>
Os métodos são iguais ao do ArrayList, ambos implementam a interface List.<br>
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
E o mistério da LinkedList? E se tivéssemos usado ArrayList na declaração do atributo aulas da classe Curso? O resultado seria exatamente o mesmo!

Então qual é a diferença? Basicamente performance. O ArrayList, como diz o nome, internamente usa um array para guardar os elementos. Ele consegue fazer operações de maneira muito eficiente, como invocar o método get(indice). Se você precisa pegar o décimo quinto elemento, ele te devolverá isso bem rápido. Quando um ArrayList é lento? Quando você for, por exemplo, inserir um novo elemento na primeira posição. Pois a implementação vai precisar mover todos os elementos que estão no começo da lista para a próxima posição. Se há muitos elementos, isso vai demorar... Em computação, chamamos isso de consumo de tempo linear.

Já o LinkedList possui uma grande vantagem aqui. Ele utiliza a estrutura de dados chamada lista ligada, e é bastante rápido para adicionar e remover elementos na cabeça da lista, isto é, na primeira posição. Mas é lento se você precisar acessar um determinado elemento, pois a implementação precisará percorrer todos os elementos até chegar ao décimo quinto, por exemplo.

Confuso? Não tem problema. Sabe o que é interessante? Você não precisa tomar essa decisão desde já e oficializar para sempre. Como utilizamos a referência a List, comprometendo-nos pouco, podemos sempre mudar a implementação, isso é, em quem damos new, caso percebamos que é melhor uma ou outra lista nesse caso em particular.