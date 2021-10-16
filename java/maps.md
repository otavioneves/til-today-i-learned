Os Maps são considerados Collections porém não é filha de Collection. Os maps trabalham com associações, que é uma forma que dado um atributo eu tenha outro atributo associado, em uma tabela, como uma relação chave-valor.<br>
```
private Map<Integer, Aluno> matriculaParaAluno = new HashMap<>();       // dado uma Matricula (um Integer), procure o aluno correspondente. O nome desse mapa ficou matriculaParaAluno e o seu tipo é HashMap<>.
```
Nesse caso que toda vez alguém adicionar um Aluno, nós colocamos no HashMap. Podemos fazer isso através do método `put`, onde dado a chave, ele salva a associação que será devolvida quando solicitada.<br>
Para solicitar utilizamos o método `get` que recebe a chave.
```
public Aluno buscaMatriculado(int numero) {
    return this.matriculaParaAluno.get(numero);
}
```
Esse método tem uma excelente performance para buscas, por também usar tabela de espalhamento.<br>
Outra implementação é o LinkedHashMap, que guarda a ordem em que foi colocado pelo put.<br>
Outra informação é que para os Maps, os valores tem que ter cada um sua chave, sem duplicar. Caso duplique a chave, o valor da chave anterior será apagado.<br>
Para acessar as chaves devemos executar:
```
Set<String> chaves = nomesParaIdade.keySet();    
for (String nome : chaves) {
    System.out.println(nome);
}
```
E para pegar os valores usamos:
```
Collection<Integer> valores = nomesParaIdade.values();
for (Integer idade : valores) {
    System.out.println(idade);
}
```
Agora só falta a terceira coleção que devolve a associação. Para tal, existe o método entrySet() e cada associação é representado através da classe Entry:
```
Set<Entry<String, Integer>> associacoes = nomesParaIdade.entrySet();
```
Repare que o método devolve um Set de Entry. Para acessar essa coleção basta usar o foreach:
```
Set<Entry<String, Integer>> associacoes = nomesParaIdade.entrySet();    
for (Entry<String, Integer> associacao : associacoes) {
    System.out.println(associacao.getKey() + " - " + associacao.getValue());
}
```