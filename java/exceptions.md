No tratamento de exceções, utilizamos palavras chaves para tratar possíveis erros que dará erro na execução do código, interrompendo o programa.<br>
Aa palavras chaves mais utilizadas no tratamento de exceções são o `try` e o `catch`.<br>
Utilizamos o try para o código que será executado, a o catch para tratar o erro. Em português: tente executar esse código, caso der tal erro, trate de tal maneira.
```
try{
    //bloco que é monitorado para erros
} catch (TipoDaException excepetion1) {
    //tratamento
}
```
```
        try{
			int[] vetor = new int[4];

			System.out.println("Antes da exception");
			
			vetor[4] = 1;
			
			System.out.println("Esse texto não será impresso");
		} catch(ArrayIndexOutOfBoundsException exception){
			System.out.println("Exceção ao acessar um índide do vetor que não existe");
		}
``` 
É possível tratar mais de um tipo de erro, com múltiplos catch:
```
try{
    //bloco que é monitorado para erros
} catch (TipoDaException1 excepetion1) {
    //tratamento do erro 1
} catch (TipoDaException2 excepetion2) {
    //tratamento do erro 2
}
```
Para capturar um erro genérico podemos usar a classe Throwable, que á superclasse dos erros e exceptions, porém utilizar isso não é uma boa prática.
```
        int[] numeros = {4, 8, 16, 32, 64, 128};
		int[] demon = {2, 0, 4, 8, 0};

		for (int i=0; i<numeros.length; i++){
			try{
				System.out.println(numeros[i] + "/" + demon[i] + " = " + (numeros[i]/demon[i]));
			}
			catch(ArithmeticException e){
				System.out.println("Erro ao dividir por zero");
			}
			catch(Throwable e){
				System.out.println("Ocorreu um erro");
			}
		}
```
<br>
É importante entender que na execução dos catchs, os catchs que vem primeiro são executados primeiro, portanto, o tratamento com exceptions específicas devem ser colocadas em primeira, e depois as de tratamento mais genérico, como abaixo.
Também é possível fazer múltiplos catchs de exceptions da mesma família, utilizando o operador ou `|`.
``
int[] numeros = {4, 8, 16, 32, 64, 128};
		int[] demon = {2, 0, 4, 8, 0};

		for (int i=0; i<numeros.length; i++){
			try{
				System.out.println(numeros[i] + "/" + demon[i] + " = " + (numeros[i]/demon[i]));
			}
			catch(ArithmeticException | ArrayIndexOutOfBoundsException  e){
				System.out.println("Aconteceu um erro");
			}
		}
``
A maneira mais correta de se capturar catchs genéricos, utilizamos o `Exception` no lugar do Throwable, conforme abaixo:
```
        int[] numeros = {4, 8, 16, 32, 64, 128};
		int[] demon = {2, 0, 4, 8, 0};
		
		for (int i=0; i<numeros.length; i++){
			
			try{
				System.out.println(numeros[i] + "/" + demon[i] + " = " + (numeros[i]/demon[i]));
			}
			catch(Exception e){
				System.out.println(e.getMessage());
				e.printStackTrace();
			}
		}
```
Essas exceções que serão capturadas são muito utilizadas para gerar logs.
<br>
Podemos também utilizar o `finally`, que pode ser usado depois do try e do catch, conforme abaixo:
```
try{
    //bloco que é monitorado para erros
} catch (TipoDaException1 excepetion1) {
    //tratamento do erro 1
} catch (TipoDaException2 excepetion2) {
    //tratamento do erro 2
} finally {
    // executado após o try ou catch
}
```
Pode ser utilizado como por exemplo na seguinte lógica: abrir arquivo, realiza leitura ou ocorre erro, realizando leitura ou ocorrendo erro fecha arquivo no finally. Pode ser usado também para fechar a conexão com um banco de dados após consulta. O finnaly é sempre executado, mesmo se o código der algum erro ou for executado corretamente, a não ser que em algum catch seja utilizado `System.exit()`.
<br>
<br>
Dentro da classe Throwable, existe algum métodos, herdados por todas as subclasses, ou seja, as exceptions. Os métodos mais utilizados são:
- getMessage(); - retorna a descrição do erro
- printStackTrace(); - imprime o stack trace do erro, ou seja, a classe e a linha que deu o erro.
<br>
Outra palavra chave utilizada é o `throw`, que é um método que pode disparar uma exception para a resposabilidade de tratamento de quem for utilizar o método, conforme no exemplo abaixo, aonde o erro é causada no método `leNumero()` e o tratamento (através do try catch) é feito no método main. Exception disparadas em tempo de execução não precisam expecificamente do throw. Isso é muito útil na construção da API e com Java Web, aonde as exceções são tratadas em um lugar específico.
```
public static void main(String[] args) {
		
		System.out.println("Entre com um número decimal");
		try {
			double num = leNumero();
			System.out.println("Você digitou " + num);
		} catch (Exception e) {
			System.out.println("Entrada inválida");
			e.printStackTrace();
		}

	}

	public static double leNumero() throws Exception {
		Scanner scan = new Scanner(System.in);
		double num = scan.nextDouble();
		return num;
	}
```
PARA NÍVEL DE VISUALIZAÇÃO DO USUÁRIO, USAMOS SEMPRE UMA MENSAGEM DE ERRO MAIS AMIGÁVEL, SEM A MENSAGEM E O STACKTRACE DO ERRO, A FIM DE AUMENTAR A SEGURANÇA DA APLICAÇÃO. O ERRO COM A MENSAGEM E O STACK TRACE É UTILIZADO À NÍVEL DE LOG.
<br>
Existem diferenças entre exception e erros. A diferença entre eles é que um erro é um erro em tempo de execução que irá causar o encerramento da aplicação (como por exemplo, OutOfMemoryError). Os erros do tipo error são não verificados e não podem ser tratados.<br>
Já as exceptions podemos tratar. As RuntimeException são exceptions causadas em tempo de execução e são não verificadas (como ArrayIndexOutOfBoundsException, NullPointerException, Arithm).<br>
As excepetions que são verificadas e o compilador já reclama e pede o tratamento, como por exemplo, as IOException e as SQLExecption.<br><br><br>
É possível também criar a própria excecption, criando uma classe para tratar uma exception que iremos escrever colocando nossa própria lógica. Essa classe criado vai extender a classe Exception. No código principal, utilizamos o `throw new` e declaramos uma nova exception com o tipo da classe que criamos.
```
public class DivisaoNaoExata extends Exception {

	private int num;
	private int dem;
	
	public DivisaoNaoExata(int num, int dem) {
		super();
		this.num = num;
		this.dem = dem;
	}

	@Override
	public String toString() {
		return "Resultado de " + num + "/" + dem + " não é um inteiro!";
	}
	
}
```
```
    public static void main(String[] args) {
		int[] numeros = {4, 8, 5, 16, 32, 21, 64, 128};
		int[] demon = {2, 0, 4, 8, 0, 2, 4};

		for (int i=0; i<numeros.length; i++){
			try{
				if (numeros[i] % 2 != 0){
					//lançar a exception aqui
					throw new DivisaoNaoExata(numeros[i], demon[i]); 
				}
				System.out.println(numeros[i] + "/" + demon[i] + " = " + (numeros[i]/demon[i]));
			}
			catch(ArithmeticException | ArrayIndexOutOfBoundsException | DivisaoNaoExata){
				System.out.println("Aconteceu um erro");
				e.printStackTrace();
			}
		}
	}
```