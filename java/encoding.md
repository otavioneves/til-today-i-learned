O encoding são versões do unicode que servem para cada Sistema Operacional. O unicode é um código universal que representa todos os caracteres, onde cada caracter tem um código único, chamado codepoint. Porém, em cada SO temos tabelas diferentes. O padrão do Windows é o windows-1252.<br>
O java utiliza o unicode, tanto que podemos imprimir um caractere através do método `codePoint`, que recebe um inteiro que indica a posição e retorna o codepoint do caracter passado.
```
String s = "C";

System.out.println(s.codePointAt(0));           // imprime 67, que é o codepoint da letra C.
```
O java se adapta ao encoding utiliza no sistema operacional e para sabermos qual o encoding padrão do SO utilizamos o método `defaultCharset`.
```
Charset charset = Charset.defaultCharset();

System.out.println(charset.displayName());
```
Podemos escolher o charSet que queremos utilizar, que receberá os bytes obtidos através do método `getBytes`, que retorna os bytes de um caracter em referência à um encoding específico.
```                               
byte[] bytes = s.getBytes("windows-1252");

bytes = s.getBytes("UTF-16");

bytes = s.getBytes(StandardCharsets.US_ASCII);      // podemos também utilizar o StandardCharsets, que recebe após a constante do encoding escolhido.
```
Ao recebermos um fluxo de bytes, temos que usar o encoding correto para transformar esses bytes em caracteres.
```
String s = "C";

byte[] bytes = s.getBytes("windows-1252");      // o array de bytes, chamado bytes, recebe os bytes do caracter "C" do encoding windows-1252
String sNovo = new String(bytes, "windows-1252");       // transformamos esse bytes em uma string
System.out.println(sNovo);          // recebemos o bytes e imprime o caracter "C"

```
Podemos também utilizar os encoding no java.io, trabalhando com as entradas e saídas. No caso a classe Scanner tem uma opção de construtor que podemos passar o arquivo e o nome do charSet desejado.
```
Scanner scanner = new Scanner(new File("contas.csv"),"windows-1252");
```