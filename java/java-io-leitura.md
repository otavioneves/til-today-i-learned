O biblioteca java.io é responsável por tratar entradas e saídas, amplamento utilizadas em aplicações Web.<br>
A maneira mais inicial de fazer o fluxo de entrada do arquivo a partir do `FileInputStream`. O FileInputStream possui vários construtores. O mais simples recebe o nome do arquivo de entrada em formato de String. Essa ação lança uma exception checked, pois o compilador não sabe se o arquivo colocado está realmente colocado na raiz do arquivo.<br>
```
FileInputStream fis = new FileInputStream("lorem.txt");
```
Esse FileInputStream tem alguns métodos, porém a melhora maneira é usar a Classe `InputStreamReader`, para ler o arquivo, que recebe um FileInputStream.
```
InputStreamReader isr = new InputStreamReader(fis);
```
A forma que faz de uma maneira melhor ainda é a `BufferedReader`, que recebe um InputStreamReader.
```
BufferedReader br = new BufferedReader(isr);

System.out.println(br.readLine());      // escreve uma linha

br.close();
```
Quandos trabalhamos com a java.io, temos que cuidar geralmente de duas Exceptions: FileNotFoundException (extends IOException) e IOException.<br>
Com tudo isso estabelecemos um fluxo de entrada, mesmo que seja mais verboso, é uma maneira de se fazer, apesar de existir uma maneira mais otimizada.
```
public static void main(String[] args) throws IOException {

	FileInputStream fis = new FileInputStream("lorem.txt");
		
	InputStreamReader isr = new InputStreamReader(fis);
		
	BufferedReader br = new BufferedReader(isr);
		
	System.out.println(br.readLine());
		
	br.close();		
}
```
O método readLine devolve um null quando não há mais conteúdo para exibir, podendo colocar essa lógico em um laço.
```
		String linha = br.readLine();
		
		while(linha != null) {
			
			System.out.println(linha);
			linha = br.readLine();
			
		}
		
		br.close();
```
- Stream: ler uma imagem, um pdf. O conceito para representar a entrada de bytes é a classe mãe InputStream.
- Reader: ler um texto.  O conceito para representar a entrada de caracteres é a classe mãe Reader.
