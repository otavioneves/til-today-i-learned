Os construtores são métodos que são rodados ao instaciarmos um objeto de uma classe. Por padrão, se não escrevermos nenhum construtor na classe, ele chama um construtor padrão, que é vazio.<br>
Podemos definir construtores que executam ações e recebem atributos, logo ao instanciarmos um objeto.
```
public class Carro{
    private int ano;
    private String modelo;
    private double preco;

    public Carro(int ano, String modelo, double preco){
        this.ano = ano;
        this.modelo = modelo;
        this.preco = preco;
    }
}
```
Para o caso de precisarmos fazer mais de um construtor, com alguma pequena diferença, devemos tomar cuidado com a duplicação de código. Para isso, no Java é possível fazer a chamada de um construtor dentro de outro e faz-se isso para evitar duplicações de códigos e regras. Afinal uma regra aplicada em um construtor normalmente será a mesma para o outro caso. Para isso usa-se o this( ) passando os parâmetros correspondentes ao construtor que se queira chamar.
```
public class Carro{
    private int ano;
    private String modelo;
    private double preco;

    public Carro(int ano, String modelo, double preco){
        this.ano = ano;
        this.modelo = modelo;
        this.preco = preco;

    public Carro(String modelo, double preco){
        this(2017, modelo, preco);
    } 
}
```
Para chamarmos o construtor de uma superclasse utilizamos a palavra chave super(), que quando usada em um construtor de uma subclasse, invoca o construtor padrão da superclasse. Podemos também chamar outros construtores da superclasse, utilizando os atributos solicitados pelo mesmo passando-os no construtor da subclasse.
```
    public Conta(){                 // construtor padrão
    }

    public Conta(int agencia, int numero){                  // construtor com atributos
        Conta.total++;
        System.out.println("O total de contas é " + Conta.total);
        this.agencia = agencia;
        this.numero = numero;
        this.saldo = 100;
        System.out.println("Estou criando uma conta " + this.numero);
    }
```
```
public class ContaCorrente extends Conta {

        public ContaCorrente(int agencia, int numero) {         // construtor da subclasse chamando um construtor com agencia e numero da superclasse
            super(agencia, numero);
        }

        public ContaCorrente() {         // construtor padrão da subclasse chamando um construtor padrão da superclasse
            super();
        }

}
```
