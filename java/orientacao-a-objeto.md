Na orientação à objeto utilizamos as classes para criarmos nossos objetos. Uma classe define atributos e métodos comuns que serão compartilhados por um objeto. Já o objeto, é a instância de uma classe.<br>
Todo objeto tem atributos, métodos e um estado.<br>
- Atributos: são características do objeto, no caso de uma caneta seria seu modelo, cor, tamanho da ponta, nível da carga, etc.;
- Métodos: seria ações realizadas pelo método, no caso de uma caneta seria escrever, rabiscar, pintar, tampar, etc.;
- Estado: status do objeto.
No exemplo da caneta, criamos uma classe "Caneta" e colocamos seus atributos e métodos:
```
public class Caneta {

	String	modelo;
	String cor;
	Double ponta;
	Integer carga;
	Boolean tampada;
	
	void tampar () {
		this.tampada = true;
	}
	void destampar () {
		this.tampada = false;
	}
	
	void rabiscar () {
		
		if (this.tampada == true) {
			System.out.println("Erro! A caneta está tampada.");
		} else {
			System.out.println("Estou rabiscando");
		}
	}
	
	void status() {
		System.out.println("Modelo: " + this.modelo);
		System.out.println("Cor: " + this.cor);
		System.out.println("Ponta: " + this.ponta);
		System.out.println("Nível da Carga: " + this.carga);
		System.out.println("Está tampada? " + this.tampada);
		
	}
	
}
```
No método main, instaciamos um objeto da classe Caneta, chamando e definindo seus atributos e chamando seus métodos.<br>
Criamos um objeto com o nome da classe, seguido do nome do objeto, igual à new e o nome da Classe seguido dos parentêsis.<br>
Para fazer referência ao objeto, utilizamos o nome do objeto, seguido do . e do atributo. Para fazer referência à um método, utilizamos o nome do objeto seguido do ., do nome do método e dos parâmetros, no caso, vazios, portando com apenas ().
```
public class Aula02 {

	public static void main(String[] args) {

		Caneta c1 = new Caneta();
		c1.cor = "Azul";
		c1.modelo = "BIC";
		c1.carga = 90;
		c1.ponta = 0.5;
		c1.destampar();
		c1.rabiscar();
		c1.status();
			
		
	}

}
```
A palavra `this` é substituído pelo objeto que chamar o método, no momento que o objeto o chama. No caso, this será substituído por `c1`.<br>
Podemos com a mesma classe criar vários objetos, conforme abaixo, onde criamos outro objeto caneta:
```
public class Aula02 {

	public static void main(String[] args) {

		Caneta c1 = new Caneta();
		c1.cor = "Azul";
		c1.modelo = "BIC";
		c1.carga = 90;
		c1.ponta = 0.5;
		c1.destampar();
		c1.rabiscar();
		c1.status();
			
		Caneta c2 = new Caneta();
		c2.cor = "Vermelha";
		c2.modelo = "Faber Castel";
		c2.carga = 100;
		c2.ponta = 0.7;
		c2.destampar();
		c2.rabiscar();
		c2.status();
	}

}
```