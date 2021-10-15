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
Para a escrita com a biblioteca java.io os processos são semelhantes ao de leitura. Também temos as divisões entre Stream e Reader, porém, os nomes das classes são referentes à escrita, Stream e Writer.
- Stream: utilizado para trabalhar com binários, imagem, pdf, etc. São eles OutputStream e FileOutputStream.
- Writer: utilizada para trabalhar com strings, arquivos de texto, etc. São eles OutputStreamWriter e BufferedReader.
```
public static void main(String[] args) throws IOException {

	OutputStream fos = new FileOutputStream("lorem2.txt");
		
	Writer osw = new OutputStreamWriter(fos);
		
	BufferedWriter bw = new BufferedWriter(osw);
		
	bw.write("Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ligula eu lectus lobortis condimentum.");
	bw.newLine();
	bw.write("auhuahauh auhauhauh uahuahu hauhu");
		
	bw.close();
		
}
```
Podemos fazer escrita e leitura no mesmo programa, e também utilizando os 3 tipos de entrada (Teclado, Rede e Arquivo) e os 3 tipos de sáida (Console, Rede e Arquivo).
```
public static void main(String[] args) throws IOException {

	Socket s = new Socket();
		
		
	InputStream fis = s.getInputStream();	//(rede)		// ou System.out (teclado)	// ou new FileInputStream("lorem.txt"); (arquivo)
	InputStreamReader isr = new InputStreamReader(fis);
	BufferedReader br = new BufferedReader(isr);
		
	OutputStream fos = s.getOutputStream();		//(rede)		// ou System.in (console)		// ou new FileOutputStream("lorem2.txt"); (arquivo)
	Writer osw = new OutputStreamWriter(fos);
	BufferedWriter bw = new BufferedWriter(osw);
	
	String linha = br.readLine();
		
	while(linha != null) {
			
		bw.write(linha);
		bw.newLine();
		linha = br.readLine();
			
	}
		
	bw.close();
	br.close();
		
}
```
A maneira mais simples de estabelecer entradas e saídas é utilizando as classes FileWriter, PrintStream e PrintWriter.
- FileWriter
```
public static void main(String[] args) throws IOException {

	FileWriter fw = new FileWriter("lorem2.txt");
		
	fw.write("Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ligula eu lectus lobortis condimentum.");
	fw.write(System.lineSeparator());		// o lineSeparator devolve uma string com as características de cada sistema operacional responsável por pular linha
	fw.write("auhuahauh auhauhauh uahuahu hauhu");
		
	fw.close();
		
}
```
OU USANDO O BUFFERED WRITER.
```
FileWriter fw = new FileWriter("lorem2.txt");
BufferedWriter bw = new BufferedWriter(fw);
		
bw.write("Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ligula eu lectus lobortis condimentum.");
bw.write(System.lineSeparator());		// o lineSeparator devolve uma string com as características de cada sistema operacional responsável por pular linha
bw.write("auhuahauh auhauhauh uahuahu hauhu");
		
bw.close();
```
- PrintStream e PrintWriter: Uma outra maneira que é mais simples ainda que o FileWriter é o PrintStream e o PrintWriter. São iguais, porém no começo do Java existia apenas os Streams, e não existia o Writer e o Reader. Com a chegada do Writet, foi crido o PrintWriter.
```
PrintStream ps = new PrintStream("lorem2.txt");
		
ps.println("Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ligula eu lectus lobortis condimentum.");
ps.println("auhuahauh auhauhauh uahuahu hauhu");
		
ps.close();
```
```
PrintWriter pw = new PrintWriter("lorem2.txt");
		
pw.println("Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam eget ligula eu lectus lobortis condimentum.");
pw.println("auhuahauh auhauhauh uahuahu hauhu");
		
pw.close();
```
Já para a leitura/entrada temos a classe Scanner.
```
Scanner scanner = new Scanner(new File("contas.csv"));

while (scanner.hasNextLine()) {
	String linha = scanner.nextLine();
	System.out.println(linha);
}
		
scanner.close();
```
O scanner possui vários métodos que facilitam muitas operações.<br>
- Podemos separar uma linha de um arquivo com o método `.split`, que recebe um regex, que pode ser algo simples, como uma vírgula.
```
		Scanner scanner = new Scanner(new File("contas.csv"));

		while (scanner.hasNextLine()) {
			String linha = scanner.nextLine();
			System.out.println(linha);
			
			String[] valores=linha.split(",");
			
			System.out.println(valores[3]);
		}
		
		scanner.close();
```
A melhora maneira é criando um novo scanner que separará os valores por vírgula separando o scanner anterior por um delimitador, através do método `useDelimiter`
```
Scanner scanner = new Scanner(new File("contas.csv"));

while (scanner.hasNextLine()) {
	String linha = scanner.nextLine();
	System.out.println(linha);
			
	Scanner linhaScanner = new Scanner(linha);
	linhaScanner.useDelimiter(",");
			
	String valor1 = linhaScanner.next();
	String valor2 = linhaScanner.next();
	String valor3 = linhaScanner.next();
	String valor4 = linhaScanner.next();
	String valor5 = linhaScanner.next();

	System.out.println(valor1+valor2+valor3+valor4+valor5);
			
	linhaScanner.close();
}
		
scanner.close();
```
Podemos também usar os outros métodos também para já fazer o parse para o tipo que queremos.
```
Scanner scanner = new Scanner(new File("contas.csv"));

while (scanner.hasNextLine()) {
	String linha = scanner.nextLine();
	System.out.println(linha);
			
	Scanner linhaScanner = new Scanner(linha);
	linhaScanner.useLocale(Locale.US);
	linhaScanner.useDelimiter(",");
			
	String valor1 = linhaScanner.next();
	int valor2 = linhaScanner.nextInt();		// parse para int
	int valor3 = linhaScanner.nextInt();		// parse para int
	String valor4 = linhaScanner.next();
	double valor5 = linhaScanner.nextDouble();		// parse para double

	System.out.println(valor1+valor2+valor3+valor4+valor5);
			
	linhaScanner.close();
	}
		
scanner.close();
```
Podemos também trabalhar com a classe Properties, criada para trabalharmos com listas de chave-valor:
```
//import deve ser java.util.Properties
Properties props = new Properties(); 
props.setProperty("login", "alura"); //chave, valor
props.setProperty("senha", "alurapass");
props.setProperty("endereco", "www.alura.com.br");
```
Podemos gravar um arquivo com o properties, utilizando o método `store`, que recebe um Stream ou um Writer.
```
Properties props = new Properties(); 
props.store(new FileWriter("conf.properties"), "algum comentário");
```
Isso cria um arquiv conf.properties.
```
#algum comentário
#Thu May 10 14:29:38 BRT 2018
senha=alurapass
login=alura
endereco=www.alura.com.br 
```
Para lermos um arquivo conf.properties podemos usar o método `load`. Uma vez lido o arquivo, podemos usar o método getProperty(key), da classe Properties, para recuperar o seu valor.
```
Properties props = new Properties();        
props.load(new FileReader("conf.properties"));

String login = props.getProperty("login");
String senha = props.getProperty("senha");
String endereco = props.getProperty("endereco");

System.out.println(login + ", " + senha  + ", " +  endereco);
```
