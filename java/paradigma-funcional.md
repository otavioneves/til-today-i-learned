O paradigma funcional é a composição de funções puras, evitando compartilhamento de estados, dados mutáveis e efeitos colaterais. É declarativa ao invés de imperativo.
- Paradigma Imperativo: é aquele que expressa o código através de comandos ao computador, nele é possível ter controle de estado dos objetos.
- Paradigma Funcional: é aquele que damos uma regra, uma declaração de como queremos que o programa se comporte.

Os lambdas obedecem o conceito do paradigma funcional, com eles podemos facilitar legibilidade do nosso código, além disso com a nova API Funcional do Java podemos ter uma alta produtividade para lidar com objetos. Primeiramente, devemos entender o que são interfaces funcionais.<br>

Restrições:
- Para criar uma lambda é preciso ter uma interface funcional atrelada à ela. Interface funcionais são interfaces que possuem apenas um método abstrato. Tem a seguinte estrutura:
```
InterfaceFuncional nomeVariavel = parametro -> logica;
```

```
public class FuncaLambda {
    public static void main(String[] args) {
        Funcao colocarPrefixoSenhorNaString = valor -> "Sr. " + valor;
        System.out.println(colocarPrefixoSenhorNaString.gerar("Joao"));
    }
}

@FunctionalInterface
public interface Funcao {
    String gerar(String valor);
}
```

O escopo da lambda é sempre definido por chaves quando tem mais de uma instrução, e ponto e vírgula no final
```
Funcao1 funcao1 = valor -> {
    System.out.println(valor);
    System.out.println(valor);
};
```
Quando é só uma instrução, não precisa.
```
Funcao1 funcao1 = valor -> System.out.println(valor);
```

- Consumer: uma interface funcional que recebe um parâmetro e não retorna nada;
- Function: uma interface funcional que recebe um parâmetro e retorna um parâmetro também.
- Predicate: uma interface funcional que recebe um parâmetros e retorna um booleano.
- Supplier: uma interface funcional que não recebe um parâmetro, e retorna algo que é definido no generics.

