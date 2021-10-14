As Function Objects são implementações que são feitas dentro deu um código aonde criamos uma classe e instanciamos um objeto apenas para usar um método, pois por exemplo, esse método precisa implementar algo, logo, isso é feito na classe. Porém o conceito de classe é ter atributos e métodos, como temos somente métodos, ela é chamada de Function Objects. Para facilitar o mesmo, podemos criar a classe ja dentro da implementação, conhecida como classe anônima.
```
    lista.sort(new Comparator<Conta>() {

        @Override
        public int compare(Conta c1, Conta c2) {

            return Integer.compare(c1.getNumero(), c2.getNumero());
                    }
        }
    );
```