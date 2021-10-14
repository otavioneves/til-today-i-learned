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