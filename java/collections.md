### List
- List, ArrayList, Vector
- Garante a ordem de inserção.
- Permite adição, atualização, leitura e remoção sem regras adicionais.
- Permite ordenação através de comparators.
Métodos:
- sort: ordenar
- set: alterar
- remove: remover
- add: adicionar
- size: quantidade de elementos da lista
- contains: contém
- isEmpty: está vazio
- clear: limpar a lista inteira
- indexOf: verifica se contém na lista, mas retorna 1 ou -1

### Queue
- Garante a ordem de inserção.
- Permite adição, atualização, leitura e remoção básica de uma fila: primeira que entra, primeiro que sai.
- Não permite mudança de orndeção.
- Sempre vamos querer trabalhar com o primeiro elemento.
Métodos
- add: adicionar
- pool: acessar o primeiro item e o remove. Pode retornar null caso a fila esteja vazia.
- peek: acessar o primeiro item mas não remove. Pode retornar null caso a fila esteja vazia.
- element: acessar o primeiro item mas não remove. Caso a fila esteja vazia, ela retorna uma vazia.
- clear: limpar a fila inteira.

### Set
- HashSet, TreeSet, LinkedHashSet.
- Possui os métodos padrões da interface Collection.
- Por padrão, não garante a ordem.
- Não permite itens repetidos.
- Não possui index.
- Permite adição e remoção normalmente. Não possui busca por item e atualização. Para leitura, apenas navegação.
- Não permite mudança de ordenação.
HashSet é utilização quando não é necessário manter uma ordenação e é bem performática. A LinkedHashSet mantém a ordem de inserção dos elementos porém é mais lenta. A TreeSet tem a arquitetura de árvore e para fazer ordenação é preciso o uso de comparators.<br>
Métodos da TreeSet:
- first: retorna o elemento topo da árvore;
- last: retorna o último elemento da árvore;
- lower: recebe por parâmetro um elemento e retorna o item abaixo na árvore;
- higher: recebe por parâmetro um elemento e retorna o item acima na árvore;
- poolFirst: além de verificar qual o elemento do topo da árvore e retira da árvore;
- poolLast: além de verificar qual o último elemento da árvore e retira da árvore;

### Map
- Map não implementa a interface Collection, portanto não possuem os mesmos métodos com as mesmas implementações das classes padrões que implementam Collection.
- HashMap, TreeMap, HashTable.
- Entrada de chave e valor.
- Permite valores repetidos, mas não permite repetição de chave.
- Permite adição, busca por chave ou valor, atualização, remoção e navegação.
- Pode ser ordenado.
Métodos de HashMap.
- put: insere ou atualiza. Ele atualiza no caso de passarmos uma chave já existente, ele atualiza o valor.
- get: retorna o valor de uma chave.
- containsKey: retorna true ou false se existe ou não uma chave.
- containsValue: retorna true ou false se existe ou não um valor.
- size: retorna o tamanho do Map.
- entrySet: retorna um Set de um objeto Entry, que possui métodos para acessar key e value;
LinkedHashMap: garante ordem de inserção.<br>
TreeMap: lógica semelhante ao TreeSet.

### Comparators
As interfaces Comparator e Comparable são utilizadas para ordenação de Collection.
- Comparable: interface para definir regra de ordenação dentro de uma classe de domínio. Por exemplo, em uma classe Estudante, iremos implementar `Comparable<Estudante>`. Essa interface tem apenas um método compareTo, que iremos sobrescrever e definir a ordem. Esse método retorna 1, -1 e 0, para maior, menor e igual.
- Comparators: interface para definir classe com regra de ordenação, é utilizada para definir uma regra de negócio de classe de Domínio, porém, o método compare dessa interface recebe dois objetos, podendo assim criarmos vários tipos de ordenação dependendo da necessidade, ordenações personalizadas.
Utilizando função lambda.
```
estudantes.sort((first, second) -> first.getIdade() - second.getIdade());
```
Em comparações mais simples, o lambda é bom de ser utilizado, mas para comparações mais complexas, deveríamos criar classes próprias para comparação.<br>
Usando métodos:
```
estudantes.sort(Comparator.comparingInt(Estudante::getIdade));
```
Utilizando a Classe Collections, o método sort.
```
Collections.sort(estudantes);
```
Nesse caso, estudante precisa implementar Comparable.<br>
Utilizando uma classe com comparator.
```
Collections.sort(estudantes, new EstudanteOrdemIdadeReversaComparator());
```
```
public class EstudanteOrdemIdadeReversaComparator implements Comparator<Estudante>{

    @Override
    public int compare(Estudante o1, Estudante o2) {
        return o2.getIdade() - o1.getIdade();
    }

}
```
Nesse caso, não somos obrigados a implementar comparable, apenas passar um Comparator.

### Optional
- Tratamento para valores que podem ser nulos.
- Possui dois estaos: presente e vazio.
- Permite que você execute operações em valores que podem ser nulos sem preocupação com NullPointerException.
```
Optional<String> optionalString = Optional.of("Valor Presente");

optionalString.ifPresentOrElse(System.out::prinln, () -> System.out.prinln("não está presente));
```
No método acima, caso o status seja presente, executa a primeira ação, caso seja vazio, executa a segunda ação.<br>
- .of(): constrói um Optional com valor passado no argumento.
- .ofNullable(): constrói um Optional com valor passado no argumento, com a diferença de que se o valor do argumento for nulo, ele lança uma NullPointerException .
- .empty: constrói um Optional vazio.
Temos também a opção com Optional de tipos primitivos, como Double, Int e Long.<br>
A implementação de Optional temos alguns outros métodos interessantes:
- isPresent(): retorna true quando é presente, e false quando é vazio.
- isFalsE(): retorna true quando é vazio, e false quando é presente.
- map(): método usado para quando queremos mostrar algum valor ou fazer alguma alteração caso tal optional seja presente.
```
optionalString.map((valor) -> valor.concat("****").ifPresent(System.out::println));
```