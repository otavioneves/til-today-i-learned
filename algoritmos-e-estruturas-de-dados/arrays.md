- Arrays: os arrays são vetores ou matrizes que armazenam mais de um dado do mesmo tipo na mesma varíavel;
```
        String[] cardapio = new String[] { "Calabresa", "Atum", "Queijo", "Presunto"};
        for(int i = 0; i < cardapio.length; i++) { // repete o laço enquanto i é menor que o tamanho do vetor
		    System.out.println("[" + i + "] " + cardapio[i]); // escreve i seguido do conteúdo de cada posição definida por i
		}
``` 
- Registros: os registros são semelhantes aos arrays, porém podem armazenar dados de mais de um tipo;
- Listas: a lista é semelhantes ao array, a lista não tem um tamanho fixo, pode durante o código ir crescendo ou diminuindo.<br>
lista Ligada: na estratura do tipo lista ligada existem nós onde cada um dos nós conhece o valor que está sendo armazenado em seu interior, além de conhecer o elemento posterior a ele.<br>
Duplamente ligada: na estrutura duplamente ligada, a lista sabe quem é o elemento anterior e o posterior.

- Pilhas: a pilha é conjunto de itens empilhados de acesso restrito, ou seja, somente um item pode ser lido ou removido por vez.<br>
LIFO UEPS: o primeiro elemento à ser retirado é o último à ser inserido (o último que entra é o primeiro que sai).<br>
FIFO PEPS: o primeiro elemente à ser retirado é o primeiro à ser inserido na pilha (o primeiro que entra é o primeiro que sai).
- Fila: a estrutura de fila admite remoção de elementos e inserção de novos sujtes à regra FIFO, o elemento removido é o que está na estrutura à mais tempo, o primeiro que entra é o primeiro que sai.
- Arvore: é uma estrutura que organiza seus elementos de forma hierárquica, onde exite um elemento que fica no topo da árvores, chamado de raiz e existem os elementos subordinados a ele, que são chamados de nós ou folhas.
- Tabela de hash: é uma estrutura que associa chaves de pesquisa à valores, que facilita uma busca em um array.
- Grafos: é uma estrutura que permitem programar a relação entre objetos. Os objetos são véstices ou nós do grafo, os relacionamentos são arestas.