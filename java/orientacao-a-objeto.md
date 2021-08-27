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
Os métodos especiais para pegar ou colocar algo em um objeto, dificultando o acesso direto aos atributos da classe.
- Getter: um metódo acessor que pega algo dentro do objeto sem acessar diretamente o objeto, garantindo maior segurança aos dados do objeto.
```
public class Caneta {

	public String modelo;

	public String getModelo() {
		return modelo;
	}
}
```
- Setter: um método modificador que coloca algo dentro do objeto sem acessar diretamento o objeto, garantindo maior segurança dos dados do objeto. Esse método precisa de um argumento para funcionar.
```
```
public class Caneta {

	public String modelo;

	public void setModelo(String modelo) {
		this.modelo = modelo;
	}
}
```
- Construct: um método construtor constrói o objeto com atributos, métodos (e podendo receber parâmetros inicias), logo ao criar o objeto, ou seja, todo objeto criado já roda o método construtor. O método construtor tem o mesmo nome da Classe.
```
public class Caneta {

	public String modelo;
	private Double ponta;
	private Boolean tampada;
	private String cor;
	
	public Caneta(String modelo, Double ponta, Boolean tampada, String cor) {
		super();
		this.modelo = modelo;
		this.ponta = ponta;
		this.tampada = tampada;
		this.cor = cor;
	}	
}
```
- OBJETO COMPLETA UTILIZANDO GETTERS, SETTER e CONSTRUCT:
public class Caneta {

	public String modelo;
	private Double ponta;
	private Boolean tampada;
	private String cor;
		
	public Caneta(String modelo, Double ponta, Boolean tampada, String cor) {
		super();
		this.modelo = modelo;
		this.ponta = ponta;
		this.tampada = tampada;
		this.cor = cor;
	}
		

	public String getModelo() {
		return modelo;
	}
	public void setModelo(String modelo) {
		this.modelo = modelo;
	}


	public Double getPonta() {
		return this.ponta;
	}
	public void setPonta(Double p) {
		this.ponta = p;
	}
	
	
	public Boolean getTampada() {
		return this.tampada;
	}
	public void setTampada (Boolean t) {
		this.tampada = t;
	}
	
	
	public String getCor() {
		return this.cor;
	}
	public void setCor(String c) {
		this.cor = c;
	}
	
	
	public void tampar() {
		this.tampada = true;
	}
	public void destampar() {
		this.tampada = false;
	}
	
	public void status() {
		System.out.println("SOBRE A CANETA:");
		System.out.println("Modelo: " + this.getModelo());
		System.out.println("Ponta: " + this.getPonta());
		System.out.println("Cor: " + this.getCor());
		System.out.println("Tampada: " + this.getTampada());
	}
	
}
- Encapsulamento: os encapsulamentos é um dos pilares da progamação orientada à objetos. Ele encapsula os dados internos e disponibiliza uma interface para o usuário.
A interface é um método abstrato que define ações mas não seus atos, ele é previsto mas não implementado, e são sempre implementados na classe do objeto. Os métodos são sempre públicos. <br>
Ao encapsular, todos os atributos do objeto ficam como privados.<br>