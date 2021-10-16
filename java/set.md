Os sets são outra classe que implementa as Collections, além de List. Os sets são conjuntos. Assim como dentro de List temos o ArrayList, dentro de Set temos o HashSet.<br>
A primeira característica de um set é que não temos garantia da ordem dos objetos colocados, diferentemente da lista, que preserva a ordem de inserção ou de modificação. Em muitos casos não temos a necessidade de preservar essa ordem.<br>
Por este motivo, os Setes não podem ser acessados por indícies, já que não tem uma ordem. Para acessar os elementos utilizamos o forEach:
```
    Set<String> alunos = new HashSet<>();
    alunos.add("Rodrigo Turini");
    alunos.add("Alberto Souza");
    alunos.add("Nico Steppat");
    alunos.add("Sergio Lopes");
    alunos.add("Renan Saggio");
    alunos.add("Mauricio Aniche");

    for (String aluno : alunos) {
        System.out.println(aluno);
    }
```
Outra características é que os sets não aceitam elementos repetidos.<br>
A maior vantagem de utilização do set é a performance em alguns casos, por exemplo, ao utilizar o método contains.
```
boolean pauloEstaMatriculado = alunos.contains("Paulo Silveira");
```
No caso do ArrayList, a inserção é bem rápida e a busca muito lenta. No caso do HashSet, a inserção ainda é rápida, embora um pouco mais lenta do que a das listas. Mas a busca é muito rápida.<br>
Além do método `unmodifiableSet()`, os sets também possuem `emptySet()`, que cria um set eternamento vazio, e `synchronizedSet()`, que transforma um set comum para um set que saiba trabalhar com thread, ou seja, threadsafe.<br>
O set uso tabela de espalhamento, por isso, ao usarmos métodos de buscas temos alguns problemas, por isso sempre que usarmos o equals precisamos usar o hashCode. Utilizando os dois, temos uma ótima performance na busca e evitamos colisões. A regra é: sempre que mudarmos o equals temos que mudar o hashCode com a mesma regra.
```
@Override
public boolean equals(Object obj) {
    Aluno outroAluno = (Aluno) obj;
    return this.nome.equals(outroAluno.nome);
}

@Override

public int hashCode(){
    return this.nome.hashCode();
}
```
Caso queiramos manter a ordem adicionada, podemos utilizar um LinkedHashSet. Por mais que consigamos manter a ordem adicionada, não podemos acessar o índice, pois ele não tem.
```
private Set<Aluno> alunos = new LinkedHashSet<>();
```
Outra forma é o TreeSet, que internamente guarda objetos que implementam Comparable, pois o TreeSet deixa esses elementos ordenados na ordem natural, podendo também receber um Comparator.
Podemos também utilizar algo mais antigo, que servem para qualque Collection, que é o método `iterator`.
```
Set<Aluno> alunos = javaColecoes.getAlunos();
Iterator<Aluno> iterador = alunos.iterator();

while (iterador.hasNext()) {            // tem um próximo parar ler?
    System.out.println(iterador.next());        // se sim, devolve o próximo Aluno.
}
```
Escolhemos um Set quando não queremos uma lista ordenada e não queremos itens repetidos.<br>
Escolhemos um List quando queremos uma lista ordenado e queremos itens repetidos.
Provavelmente, caso a modelagem do sistema ainda não esteja bem definida, o desenvolvedor irá utilizar a interface Collection. Dessa maneira, terá acesso aos métodos básicos de todas as implementações, como size(), add(), remove() e contains(). Conforme for sentindo necessidade em algo específico, o desenvolvedor fará poucas mudanças em seu código.<br>
Caso sinta necessidade de fazer uma requisição a um elemento específico através da sua posição, trocará de Collection para List.<br>
Caso perceba que ordem não importa, porém é necessária uma busca bem rápida (e sem repetições), um Set é mais apropriado.<br>
Enquanto não sentir essa necessidade, provavelmente a Collection será a melhor escolha.