As classes internas são as classes criadas dentro de uma outra classe. A classe interna tem acesso aos atributos das classes internas. A classe interna é mais utilizada quando precisamos declarar uma classe que não será usada mais em nenhuma parte do projeto, apenas na classe externa. As classes internas são muito utilizadas para acesso à banco de dados pelo Hibernate/JPA, quando precisamos usar chaves primárias compostas.
```
	private String texto = "texto externo";
	
	public class Interna{
		
		private String texto = "texto interno";
		
		    public void imprimeTexto(){

			    System.out.println(texto); //imprime o texto interno
			    System.out.println(Externa.this.texto); //imprime o texto externo

		    }
	    }
    }
```
Para instanciar uma classe interna, primeiro precisamos instanciar a classe externa e depois a interna, ficando com `externa.new Interna`.
```
	public static void main(String[] args){
		
		Externa externa = new Externa();
		Interna interna = externa.new Interna();
		
		interna.imprimeTexto();
	}
```

A classe local são classes declaradas dentro de um método, tendo escopo apenas dentro desse próprio método. As classes locais podem ser muito utilizadas para simular actions do swing.

```
public class Externa2 {

	public void metodoQualquer(){

		class ClasseLocal{

			private String texto = "texto classe local";

			public void imprimeTexto(){
				System.out.println(texto);
			}
		}

		ClasseLocal local = new ClasseLocal();

		local.imprimeTexto();
	}

	public static void main(String[] args){

		Externa2 externa = new Externa2();

		externa.metodoQualquer();
	}
}
```

Outro tipo é a classe anônima, que é uma classe que a gente instancia mas muda seu comportamento enquanto está instanciando. Podemos sobrescrever elementos da classe. Classes anônimas pode implementar uma interface, instanciando uma interface como classe anônima. As classes anônimas são muito utilizadas com collections, para comparar objetos, entre outros.

```
public class Anonima {

	public void imprimeTexto(){
		System.out.println("qualquer texto");
	}
	
	public static void main(String[] args){
		
		Anonima anonima = new Anonima(){
			public void imprimeTexto(){
				System.out.println("qualquer texto que foi sobrescrito");
			}
		};
		
		anonima.imprimeTexto();
		
		//usando interface
		Texto texto = new Texto() {
			@Override
			public void imprimeTexto() {
				System.out.println("qualquer texto - interface");
			}
		};
		
		texto.imprimeTexto();
	}
```
