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
Ao encapsular, todos os atributos do objeto ficam ou como privados, ou como publicos ou protegidos, dependendo da necessidade.<br>
No exemplo abaixo, nosso programa principal instancia lutadores, através da classe Lutador, e os objetos se relacionam por agregação na classe Luta.
```
package aula07;
\\ programa principal
public class Aula07 {

	public static void main(String[] args) {

		Lutador l[] = new Lutador[6];
		
		l[0] = new Lutador("Preety Boy","França", 31, 11,2,1,1.75,68.9) ;
		
		l[1] = new Lutador("Script","Brasil",29,14,2,3,1.68,57.8);
		
		l[2] = new Lutador("Snapshadow","EUA",35,12,2,1,1.65,80.9);
		
		l[3] = new Lutador("Dead Code","Austrália",28,13,0,2,1.93,81.6);
		
		l[4] = new Lutador("UFOCobol","Brasil",37,5,4,3,1.70,119.3);
		
		l[5] = new Lutador("Nerdaart","EUA",30,12,2,4,1.81,105.7);	
						
		for (int i = 0 ; i<6;i++) {
			l[i].apresentar();
			l[i].status();
		}
		
		Luta UEC01 = new Luta();
		UEC01.marcarLuta(l[0], l[1]);
		UEC01.lutar();
	}

}
```
```
package aula07;
\\ classe do objeto Lutador
public class Lutador {

	private String nome, categoria, nacionalidade;
	private Integer idade, vitorias, derrotas, empates;
	private Double altura, peso;
	
	public void ganharLuta() {
		this.setVitorias(this.getVitorias()+1);	
	}
	
	public void perderLuta() {
		this.setDerrotas(this.getDerrotas()+1);
	}
	
	public void empatarLuta() {
		this.setEmpates(this.getEmpates()+1);
	}
	
	public void apresentar () {
		System.out.println();
		System.out.println("--------------"+ this.getNome() + "-----------------");
		System.out.println("Nome: " + this.getNome());
		System.out.println("Origem: " + this.getNacionalidade());
		System.out.println(this.getIdade()+" anos");
		System.out.println(this.getAltura() + "m de altura");
		System.out.println("Pesando" + this.getPeso() + "Kg");
		System.out.println("Ganhou " + this.getVitorias());
		System.out.println("Perdeu " + this.getDerrotas());
		System.out.println("Empatou " + this.getEmpates());
		System.out.println("----------------------------------------------------");
		System.out.println();
	}
	
	public void status() {
		System.out.print(this.getNome());
		System.out.print(" é um peso " + this.getCategoria());
		System.out.print(". Ele tem " + this.getVitorias() + " vitórias, ");
		System.out.println(this.getDerrotas() + " derrotas e ");
		System.out.println(this.getEmpates() + " empates. ");
	}
	
	
	public Lutador(String nome, String nacionalidade, Integer idade, Integer vitorias,
			Integer derrotas, Integer empates, Double altura, Double peso) {
		super();
		this.setNome(nome);
		this.setNacionalidade(nacionalidade);
		this.setIdade(idade);
		this.setVitorias(vitorias);
		this.setDerrotas(derrotas);
		this.setAltura(altura);
		this.setPeso(peso);
		this.setEmpates(empates);
	}
		
	public String getNome() {
		return nome;
	}
	public void setNome(String nome) {
		this.nome = nome;
	}
	public String getCategoria() {
		return categoria;
	}
	private void setCategoria() {
		if(this.peso < 52.2) {
			categoria = "Inválido";
		} else if (this.peso<=70.3){
			categoria = "Leve";
		} else if (this.peso<=83.9) {
			categoria = "Médio";
		} 	else if (this.peso<=120.2) {
			categoria = "Pesado";
		} 	else {
			categoria = "Inválido";
		}
	}
	public String getNacionalidade() {
		return nacionalidade;
	}
	public void setNacionalidade(String nacionalidade) {
		this.nacionalidade = nacionalidade;
	}
	public Integer getIdade() {
		return idade;
	}
	public void setIdade(Integer idade) {
		this.idade = idade;
	}
	public Integer getVitorias() {
		return vitorias;
	}
	public void setVitorias(Integer vitorias) {
		this.vitorias = vitorias;
	}
	public Integer getDerrotas() {
		return derrotas;
	}
	public void setDerrotas(Integer derrotas) {
		this.derrotas = derrotas;
	}
	public Integer getEmpates() {
		return empates;
	}
	public void setEmpates(Integer empates) {
		this.empates = empates;
	}
	public Double getAltura() {
		return altura;
	}
	public void setAltura(Double altura) {
		this.altura = altura;
	}
	public Double getPeso() {
		return peso;
	}
	public void setPeso(Double peso) {
		this.peso = peso;
		this.setCategoria();
	}
}
```
```
package aula07;

import java.util.Random;

public class Luta {

	private Lutador desafiado;
	private Lutador desafiante;
	private Integer rounds;
	private Boolean aprovada;
	
	public void marcarLuta(Lutador l1, Lutador l2) {
		
		System.out.println();
		System.out.println("Marcando a luta...");
		System.out.println();
		if (!(l1.getCategoria() == l2.getCategoria())) {
			System.out.println("Lutadores não são da mesma categoria.");
			this.setAprovada(false);
			this.setDesafiado(null);
			this.setDesafiante(null);
		}	else if (l1.equals(l2)) {
			System.out.println("Lutadores são iguais.");
			this.setAprovada(false);
			this.setDesafiado(null);
			this.setDesafiante(null);
		} else {
			this.setAprovada(true);
			this.setDesafiado(l1);
			this.setDesafiante(l2);
		}
		
		System.out.println();
	
	}
		
	public void lutar() {
		if (this.getAprovada().equals(true)) {
			System.out.println("#####DESAFIADO#####");
			this.desafiado.apresentar();
			System.out.println("#####DESAFIANTE#####");
			this.desafiante.apresentar();
			
			Random aleatorio = new Random();
			int vencedor = aleatorio.nextInt(3);		
			
			switch (vencedor) {
			case 0:
				System.out.println("Empatou!");
				this.desafiado.empatarLuta();
				this.desafiante.empatarLuta();
				break;
			case 1:
				System.out.println(this.desafiado.getNome() + " ganhou!");
				this.desafiado.ganharLuta();
				this.desafiante.perderLuta();
				this.desafiado.apresentar();
				break;
			case 2:
				System.out.println(this.desafiante.getNome()+ " ganhou!");
				this.desafiado.ganharLuta();
				this.desafiante.perderLuta();
				this.desafiante.apresentar();
				break;
			default:
				break;
			}	
		}
		else {
			System.out.println("Luta não aprovada.");
		}
	}
	public Lutador getDesafiado() {
		return desafiado;
	}

	public void setDesafiado(Lutador desafiado) {
		this.desafiado = desafiado;
	}

	public Lutador getDesafiante() {
		return desafiante;
	}

	public void setDesafiante(Lutador desafiante) {
		this.desafiante = desafiante;
	}

	public Integer getRounds() {
		return rounds;
	}

	public void setRounds(Integer rounds) {
		this.rounds = rounds;
	}

	public Boolean getAprovada() {
		return aprovada;
	}

	public void setAprovada(Boolean aprovada) {
		this.aprovada = aprovada;
	}
}
```

- Interface: uma interface é uma classe aonde se cria métodos, porém não se define os mesmos, a fim de serem chamados e definidos suas ações na classe que gerará um objeto.
```
package aula06;

public interface Controlador {

	public abstract void ligar();
	public abstract void desligar();
	public abstract void abrirMenu();
	public abstract void fecharMenu();
	public abstract void maisVolume();
	public abstract void menosVolume();
	public abstract void ligarMudo();
	public abstract void desligarMudo();
	public abstract void play();
	public abstract void pause();
	
}
```
```
package aula06;

public class Controle implements Controlador{

	private Integer volume;
	private Boolean ligado;
	private Boolean tocando;
	public Controle() {
		super();
		this.setVolume(50);
		this.setLigado(true);
		this.setTocando(false);
	}
	
	
	private Integer getVolume() {
		return volume;
	}
	private void setVolume(Integer volume) {
		this.volume = volume;
	}
	private Boolean getLigado() {
		return ligado;
	}
	private void setLigado(Boolean ligado) {
		this.ligado = ligado;
	}
	private Boolean getTocando() {
		return tocando;
	}
	private void setTocando(Boolean tocando) {
		this.tocando = tocando;
	}

	@Override
	public void ligar() {
		this.setLigado(true);
		System.out.println("Ligado");
	}

	@Override
	public void desligar() {
		this.setLigado(false);
	}

	@Override
	public void abrirMenu() {
		if (this.getLigado().equals(false)){
			System.out.println("TV desligada");
		} else {
		
		System.out.println();
		System.out.println("--------------MENU--------------");
		System.out.println("Está ligado? " + this.getLigado());
		System.out.println("Está tocando " + this.getTocando());
		System.out.println("Volume: " + this.getVolume());

		
		for (int i=0;i<=this.getVolume();i+=10) {
			System.out.print("|");
		}
		System.out.println();
		System.out.println("-------------------------------");
		System.out.println();
		
		}
	}

	@Override
	public void fecharMenu() {
		if (this.getLigado().equals(false)){
			System.out.println("TV desligada");
		} else {
		System.out.println("Fechar Menu");
		}
	}


	@Override
	public void maisVolume() {
		if(this.getLigado()&&this.getVolume()<100) {
			this.setVolume(this.getVolume()+10);
			System.out.println("Volume: " + this.getVolume());
		} else if (this.getVolume().equals(100)){
			System.out.println("Volume no máximo");
		} else {
			System.out.println("TV Desligada");
		}
	}


	@Override
	public void menosVolume() {
		if (this.getLigado()&&this.getVolume()>0) {
			this.setVolume(this.getVolume()-10);
			System.out.println("Volume: " + this.getVolume());
		} else if (this.getVolume().equals(0)) {
			System.out.println("Volume no mínimo");			
		} else {
			System.out.println("TV Desligada");
		}
	}


	@Override
	public void ligarMudo() {
		if (this.getLigado()&&this.getVolume()>0) {
			this.setVolume(0);
			System.out.println("Mudo");
		} else if (this.getVolume().equals(0)) {
			System.out.println("O volume já está em 0.");
		} else {
			System.out.println("A TV está desligada.");
		}
	}


	@Override
	public void desligarMudo() {
		if (this.getLigado()&&this.getVolume().equals(0)) {
			this.setVolume(50);
			System.out.println("Desligado Mudo. Volume " + this.getVolume());
		} else if (this.getLigado().equals(false)) {
			System.out.println("A TV está desligada.");
		} else {
			System.out.println("TV já está com volume.");

		}
			
		
	}

	
	@Override
	public void play() {
		if (this.getLigado().equals(false)){
			System.out.println("TV desligada");
		} else {
		if (this.getLigado()&& !(this.getTocando())) {
			this.setTocando(true);
		}
		}
	}

	@Override
	public void pause() {
		if (this.getLigado().equals(false)){
			System.out.println("TV desligada");
		} else {
		if (this.getLigado()&& this.getTocando())
			this.setTocando(false);
		}
	}
	
}

```
