### Java 9
- Factory Method para Coleções: já popular a collection na criação
```
List<String> = List.of("nome1","nome2","nome3");
```
- Fluxo Reativo: o fluxo reativo inverte o processo normal, o webService que vai solicitar a quantidade de serviços que irá processar, e não o programa que irá mandar sem limites.
- Java Modular: o módulo tem alguns benefícios como encapsulamento de APIs, resoluções de problemas para o ClassPath.

### Java 10
- Inferência de variável: utilizar a palavra chave var, e o java irá inferir qual seria o tipo da varíavel.
- Interface para garbage collector.

### Java 11
- Execução de um arquivo java com um único comando: não é mais necessário utilizar o comando javac, pode ir diretamente no comando java.
- HttpCliente: nova API, com suporte para http2, novos métodos, requisições assíncronas, etc.

### Java 12
- Inclusão do novo garbagge collector

### Java 13
- Mudanças na Socket API.
- Text Blocks: criação de um bloco, identificado por aspas triplas no ínicio e no fim, que facilita por exemplo o pular linha.

### Java 14
- Helpful NullPointerExceptions: auxilia para encontrar aonde está dando NullPointerException no programa, sendo uma solução ao debug para encontrar o nullpointer.
- Switch Expressions: melhoria no switch case, utilizando lambdas:
```
switch (nome){
    case "nome1","nome2","nome3" -> System.out.println("Achou o nome: " + nome);
    default -> System.out.println("Não achou nenhum nome");
}
```
- Records: utilizado para facilitar escritas de DTO.