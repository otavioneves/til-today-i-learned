O conceito de polimorfisco na Orientação a Objeto é que algo pode ser feito de formas diferentes.<br>
Todo método tem uma assinatura, que é a quantidade e os tipos dos parâmetros.<br>
Os principais tipos de polimorfismo são o de sobreposição e o de sobrecarga.
- Sobreposição: mesma assinatura, classes diferentes;
```
package aula13;

public class Aula13 {

	public static void main(String[] args) {

		Cachorro x = new Cachorro();
		x.emitirSom();
		
		Lobo z = new Lobo();
		z.emitirSom();
		
		Mamifero y = new Mamifero ();
		y.emitirSom();
	}
}
```
```
package aula13;

public class Mamifero extends Animal {

	protected String corPelo;

	@Override
	public void emitirSom() {
		System.out.println("Som de Mamífero");
	}
}
```
```
package aula13;

public class Lobo extends Mamifero {
	
	@Override
	public void emitirSom() {
		System.out.println("Auuuuuuu");
	}
	
}
```
```
package aula13;

public class Cachorro extends Mamifero {

	@Override
	public void emitirSom() {
		System.out.println("Au,au,au!");
	}	
}
```
- Sobrecarga: assinaturas diferentes, mesma classe.
```
package aula13;

public class Aula13 {

	public static void main(String[] args) {

		Cachorro c = new Cachorro ();
		
		c.reagir("Olá");
		c.reagir("Vai apanhar");
		c.reagir(11, 45);
		c.reagir(19, 00);
		c.reagir(true);
		c.reagir(false);
		c.reagir(2,12.5);
		c.reagir(17,4.5);
	}
}
```
```
package aula13;

public class Cachorro extends Mamifero {
	
	public void reagir (String frase) {
		if (frase=="Toma Comida" || frase =="Olá") {
			System.out.println("Abanar e Latir");
		} else {
			System.out.println("Rosnar");
		}
	}
	
	
	public void reagir (int hora, int min) {
		if (hora<12) {
			System.out.println("Abanar");
		} else if (hora>18) {
			System.out.println("Ignorar");
		} else {
			System.out.println("Abanar e Latir");
		}
	}
	
	public void reagir(Boolean dono) {
		 if (dono) {
			 System.out.println("Abanar");
		 } else {
			 System.out.println("Latir");
		 }
		
	}
	
	public void reagir (int idade, double peso) {
		if (idade <5) {
			if (peso < 10) {
				System.out.println("Abanar");
			} else {
				System.out.println("Latir");
			}
		}  else {
			if (peso < 10) {
				System.out.println("Rosnar");
			} else {
				System.out.println("Ignorar");
			}
		}
	}	
}
```