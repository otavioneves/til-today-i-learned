Podemos fazer ordenação de listas através do método `.sort`. Com o sort, podemos usar a classe Comparator para ordenar segundo algum critério. O método `compare` dessa classe geralmente é aplicado em uma classe separada do código principal, com a regra de ordenação. O código pode ser o seguinte: No caso, estamos querendo ordenar uma lista de Contas.
```
class NumeroDaContaComparator implements Comparator<Conta> {

        @Override
        public int compare(Conta c1, Conta c2) {

                if(c1.getNumero() < c2.getNumero()) {
                    return -1;
                }

                if(c1.getNumero() > c2.getNumero()) {
                    return 1;
                }

            return 0;
        }
}
```
```
public class Teste {

        public static void main(String[] args) {

        //Código omitido

        List<Conta> lista = new ArrayList<>();
        lista.add(cc1);
        lista.add(cc2);
        lista.add(cc3);
        lista.add(cc4);

        foreach (Conta conta : lista) {
            System.out.println(conta);
        }

        NumeroDaContaComparator comparator = new NumeroDaContaComparator();

        System.out.println("---------");

        lista.sort(comparator);

        for (Conta conta : lista) {
            System.out.println(conta);
        }

    }

}
```
- Podemos também ordenar Strings, através do método `compareTo()` que recebe duas strings.
```
class TitularDaContaComparator implements Comparator<Conta> {

        @Override
        public int compare(Conta c1, Conta c2) {

                String nomeC1 = c1.getTitular().getNome();
                String nomeC2 = c2.getTitular().getNome();
                return nomeC1.compareTo(nomeC2);
        }
}
```
```
for (Conta conta : lista) {
    System.out.println(conta);
}

TitularDaContaComparator titularComparator = new TitularDaContaComparator();
lista.sort(titularComparator);

for (Conta conta : lista) {         // ordenado
    System.out.println(conta + ", " + conta.getTitular().getNome());
}
```
- Podemos usar os Wrappers para chamar o método `compare`.
```
class NumeroDaContaComparator implements Comparator<Conta> {

        @Override
        public int compare(Conta c1, Conta c2) {

            return c1.getNumero() - c2.getNumero();
        }
}
```
- Outra maneira mais enxuta pra fazer essa ordenação é:
```
lista.sort(new TitularDaContaComparator());
```
- Com a classe Collections podemos também fazer o sort passando a List e um Comparator:
```
Collections.sort(lista, new NumeroDaContaComparator());
```
- Podemos utilizar a ordem natural, implementando o Comparable da classe java.lang. Nesse caso, podemos usar o método compareTo.

```
public abstract class Conta extends Object implements Comparable<Conta> {

                protected double saldo;
                private int agencia;
                private int numero;
                private Cliente titular;
                private static int total = 0;

//Código omitido

// ordenando pelo saldo

                @Override
                public int compareTo(Conta outra) {
                    return Double.compare(this.saldo, outra.saldo);
                }

}
```
```
public class Teste {

//Código omitido

// ordenando pelo saldo
        lista.sort(null);

        for (Conta conta : lista) {
                System.out.println(conta + ", " + conta.getTitular().getNome());
        }

}
```