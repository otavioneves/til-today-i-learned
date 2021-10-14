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
