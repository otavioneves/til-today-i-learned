A palavra chave static, principalmente dentro de classes que tem objetos declarados, transforma um atributo que seria de cada objeto criado em um atributo da classe. O atributo vira compartilhado entre as instâncias, e o mesmo serve para os métodos. Uma desvantagem de se usar o static, é que dentro de um método static não podemos acessar um atributo de uma instância com o this.
```
public class Conta { 
    private double saldo;
    private int agencia;
    private int numero; 
    private Cliente titular; 
    private static int total;

    public Conta(int agencia, int numero) { 
        Conta.total ++;
        System.out.println("o total de contas é " + Conta.total);
        this.agencia = agencia; 
        this.numero = numero; 
        System.out.println("estou criando uma conta " + this.numero); 
    }
```
```
    public static void main(String[] args) { 
        Conta conta = new Conta(1337, 24226); 
        Conta conta2 = new Conta(1337, 16549);
        Conta conta3 = new Conta(2112, 14660);

        System.out.println(Conta.total);
```