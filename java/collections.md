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
HashSet é utilização quando não é necessário manter uma ordenação e é bem performática. A LinkedHashSet mantém a ordem de inserção dos elementos porém é mais lenta. A TreeSet tem a arquitetura de árvore e para fazer ordenação é preciso o uso de comparators.