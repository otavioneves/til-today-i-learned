Os enumeradores é semelhante a um tipo de constante, porém com funcionalidades extras. No enum o tipo dele é o nome dele e damos um nome ao enum criado, seguido do tipo ponto e qual enum.
`TipoDaVariavel nome = TipoDaVariavel.ENUM`

A vantagem de usar enum no java é ao declarar atributos, dando o controle que só será atribuído valores que foram declarados como enum.
```
public enum DiaSemana {
	
	SEGUNDA, TERCA, QUARTA, QUINTA, SEXTA, SABADO, DOMINGO;
}
```
```
    public static void main(String[] args) {

		System.out.println();
		
		usandoEnum();
	}
	
	private static void usandoEnum(){
		
		DiaSemana segunda = DiaSemana.SEGUNDA;
		DiaSemana terca = DiaSemana.TERCA;
		DiaSemana quarta = DiaSemana.QUARTA;
		DiaSemana quinta = DiaSemana.QUINTA;
		DiaSemana sexta = DiaSemana.SEXTA;
		DiaSemana sabado = DiaSemana.SABADO;
		DiaSemana domingo = DiaSemana.DOMINGO;
		
		System.out.println("Teste utilizando enum no Java");
		imprimeDiaSemana(segunda);
		imprimeDiaSemana(terca);
		imprimeDiaSemana(quarta);
		imprimeDiaSemana(quinta);
		imprimeDiaSemana(sexta);
		imprimeDiaSemana(sabado);
		imprimeDiaSemana(domingo);
	}
	
	private static void imprimeDiaSemana(DiaSemana dia){
		switch (dia) {
		case SEGUNDA:
			System.out.println("Segunda-feira");
			break;
		case TERCA:
			System.out.println("Terça-feira");
			break;
		case QUARTA:
			System.out.println("Quarta-feira");
			break;
		case QUINTA:
			System.out.println("Quinta-feira");
			break;
		case SEXTA:
			System.out.println("Sexta-feira");
			break;
		case SABADO:
			System.out.println("Sábado");
			break;
		case DOMINGO:
			System.out.println("Domingo");
			break;
		}
	}
```
- É possível utilizar os enums como classes, com construtores e métodos. O construtor dos enums não usam modificador de acesso, ficam com o default.
- Não precisamos utilizar o `new` para instanciar o enum. Para instanciarmos o enum, primeiro criamos um construtor na classe, depois ao definir o enum e chamar o construtor, o enum já é criado, não sendo necessário utilizar o new.
- Os enums não podem ter herança, pois eles já extends a java.lang.Enum.
- O enum pode ser declarado dentro de uma classe, mais indicado para quando o Enum não será reutilizado em outro lugar, conforme abaixo:
```
public class Formulario {
	
	enum Genero {
		FEMININO('F'), MASCULINO('M');
		
		private char valor;
		
		Genero(char valor){
			this.valor = valor;
		}
	}

	private String nome;
	private Genero genero;
}
```
Podemos utilizar também alguns métodos. Como o enum é basicamente uma coleção de constantes, podemos iterar um enum, criando um array do tipo do enum. O método `values()` retorna um array de todos os valores de dentro do enumerador.
```
        DiaSemana[] dias = DiaSemana.values(); \\o DiaSemana.values() cria retorna os valores e colocam no vetor dias[], cada enum em uma posição.

		for (int i=0; i<dias.length; i++){
			System.out.println(dias[i]);
		}
		
		for (DiaSemana dia : DiaSemana.values()){
			System.out.println(dia);
		}
```
Outro método é o método valueOf, utilizado para obter o próprio valor do enum. Conseguimos obter o valor do enum através de uma string. O método value of vai buscar a string e retorna o próprio enumerador. Se você não souber qual é o enum, mas você tem o valor em uma string, você pode avaliar essa string transformando em uma instância de um enumerador.
```
		DiaSemana dia = Enum.valueOf(DiaSemana.class, "DOMINGO");
		
		System.out.println(dia);
```
O enum pode ter métodos abstratos. Para ter os métodos ele pode implementar uma interface ou ter os próprios métodos abstratos.
```
    CPF {
		@Override
		public String geraNumeroTeste() {
			return GeraCpfCnpj.cpf();
		}
	}, CNPJ {
		@Override
		public String geraNumeroTeste() {
			return GeraCpfCnpj.cnpj();
		}
	};
	
	public abstract String geraNumeroTeste(); \\nessa caso estamos criando um método próprio
```