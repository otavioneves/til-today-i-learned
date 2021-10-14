O Vector é uma implementação de List que é thread safe.<br>
No dia a dia não se usa muito o vector, pois é um pouco mais custoso em relação ao desempenho. O Vector utiliza arrays por trás dos panos, semelhantes ao ArrayList. Uma caracterítica da List é que ela aceita duplicadas, ou seja, adicionar em dois elementos da lista com a mesma referência. Caso queiramos que não tenha duplicados, temos que escrever uma lógica que utiliza o `.contains`. Ela também implementa a interface Collections, além da List.
```
List<Conta> lista = new Vector<Conta>();        //thread safe
```
As listas também só guardam referências (String, Classes, Wrappers, etc), não guardam primitivos (como int, double, boolean, etc). Caso queiramos adicionar um item primitivo o java utiliza o Autoboxing, para transformar esse tipo primitivo em uma Referência.
```
String[] nomes = new String[5];

int idade = 29;
Integer idadeRef = new Integer(29);
List<Integer> numeros = new ArrayList<Integer>();

numeros.add(idade);     // inválido, pois idade é um int, tipo primitivo

numeros.add(29);        // válido, estamos adicionando um 29, que seria um int, tipo primitivo, Autoboxing
```