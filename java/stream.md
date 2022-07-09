Stream API: Manipulação de coleções com o paradgima funcional de forma paralela. O funcionamento dela é imutável, ou seja, ela não manipula a origem do dado, mas cria uam nova coleção. Para os exemplos abaixo, consideraramos uma List populada.
```
List<String> estudantes = new ArrayList();
```
Para acessar os métodos da Stream API é através do método stream().
- Mapping: retorna uma coleção com mesmo tamanho da origem com os elementos alterados. Transforma os elementos de uma coleção em outros tipos, e depois coleciona novamente.
```
estudantes.stream().map(estudante -> estudantes.concat(" - ").concat(String.valueOf(estudante.length))).collect(Collectors.toList)      // a nova coleção terá além do nome dos estudantes, agora terá o nome concatenado com o número de caracteres do nome.
```

- Filtering: retorna uma coleção igual ou menor que a coleção origem, com os elementos intactos, de acorda com uma regra. O filter recebe uma regra e sempre retorna true or false, isso pra cada elemento da coleção origem. Caso seja true, esse elemento irá ser adicionado à uma nova coleção. Após passar por todos os elementos, o método retorna essa nova coleção com esses elementos filtrados.
```
estudantes.stream().filter((estudantes) -> estudante.toLowerCase().contains("r")).collect(Collector.toList));       // filtra dentre os estudantes aqueles que tem letra r, e coleciona em uma nova coleção list.
```

- ForEach: executa uma determinada lógica para cada elemento, retornando nada.
```
estudantes.stream().forEach(System.out::println);
```

- Peek: executa uma determinada lógica para cada elemento, retornando a própria coleção.
```
estudantes.stream().peek(System.out::println).collect.(Collectors.toList()));       // executa o sysout pra cada elementa da coleção e depois retorna a mesma coleção.
```

- Counting: retorna um inteiro que representa a contagem de elementos.
```
estudantes.stream().count();
```

- Grouping: retorna uma coleção agrupada de acordo com a regra definida.
```
.collect(Collectors.joining(", "))     // retorna uma string dos elementos de uma coleção, somando pela delimitador que passarmos como atributo

.collect(Collectors.toSet())        // retorna um Set.

.collect(Collector.groupingBy(estudante -> estudante.substring(estudante.indexOf("-") + 1)))       // agrupa de acordo com uma regra, no caso, agrupa a partir do primeiro elemento após o traço.
```

- Max e min: recebe um algoritmo de comparação, um comparator, e retorna o maior e o menor em referência essa regra de comparação.
```
estudantes.stream().max(Comparator.comparingInt(String::length));       // retorna a maior string da coleção estudantes.
```

- Limit: limita a um número de elementos que passarmos, podendo depois colecionar também.
```
estudantes.stream().limit(3).collect(Collector.toList);
```

- allMatch: faz uma verificação em todos os elementos da coleção, caso todos elementos se encaixem na verificação, retorna true, se não, retorna false.
```
estudantes.stream().allMatch((elemento) -> elemento.contains("W"));
```

- anyMatch: faz uma verificação em todos os elementos da coleção, caso no mínimo um elemento se encaixe na verificação, retorna true, se não tiver nenhum, retorna false.
```
estudantes.stream().anyMatch((elemento) -> elemento.contains("W"));
```

- noneMatch: faz uma verificação em todos os elementos da coleção, caso nenhum elemento se encaixe na verificação, retorna true, se não tiver algum, retorna false.
```
estudantes.stream().noneMatch((elemento) -> elemento.contains("W"));
```

- findFirst: retorna um Optional, ou seja, caso seja null ele não retorna exception.
```
estudantes.stream().findFirst().ifPresent(System.out:println);
```

### Operação encadeada
Esses métodos trabalham de forma paralela, ou seja, o peek e o map acontecem de forma paralela.
```
estudantes.stream()
.peek(System.out::println)      // mostra a coleção
.map (estudante ->
        estudante.concat(" - ").concat(String.valueOf(estudante.length)))       // concatena o nome com o tamanho do nome
.peek(System.out::println)      // mostra o resultado do map
.fiter((estudante) -> estudante.toLowerCase().concat("r"))      // filtra os nomes que tem r
.collect(Collector.toList())        // coleciona em uma nova lista
```