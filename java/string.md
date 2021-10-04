Existem alguns modos de trabalharmos com as strings.<br>

### Criando uma String
Com a String é uma classe, podemos criar uma através do métodos `new`.
```
        String vazia = new String(); //String vazia ""
		System.out.println(vazia);

		String java = new String("JAVA"); // criando uma nova variavel chamada java, do tipo string, com o conteúdo "Java"
		System.out.println(java);
		
		String java1 = new String(java); // criando uma nova variavel chamada java1, do tipo string, com o conteúdo sendo referenciado pela varíavel java
		System.out.println(java1);
```
A string também pode receber uma array de chars.
```
		char[] charsJava = {'J', 'A', 'V', 'A'}; // array de characters
		String java2 = new String(charsJava); // criando uma nova variavel chamada java2, do tipo string, com o conteúdo recebendo o array charsJava
		System.out.println(java2);

        char[] abcdef = {'A', 'B', 'C', 'D', 'E', 'F'};
		String abc = new String(abcdef, 0, 3); // criando uma nova variavel chamada abc, do tipo string, que recebe o conteúdo do array abcdef, porém recebendo apenas com os 3 primeiros caracteres desse array.
		System.out.println(abc);
```
Podemos também utilizar um array de bytes, onde cada byte é referente à um número na tabela ASCII.
```
        byte[] ascii = {65, 66, 67, 68, 69};
		String abcde = new String(ascii);
		System.out.println(abcde);

        String bcd = new String(ascii, 1, 3); // da mesma maneira, podemos pegar apenas os itens do array dos bytes.
		System.out.println(bcd);
```
A forma mais comum de criar uma string é a atribuição simples.
```
		String java3 = "JAVA";
		System.out.println(java3);
```
A maior diferença entre criar pela atribuiçã simples e pelo construtor com o método new é que no segundo caso, ao criar a varíavel com o construtor ele reserva um endereço de memória específico para cada string criada, mesmo que os seus conteúdos sejam os mesmos. Já na atribuição simples, caso as strings tenham o mesmo conteúdo, as duas varíaveis ficaram guardadas no mesma espaço de memória.<br>

### Concatenando Strings
A concatenacao é a adição, junção, de strings.
```
        String curso = "Curso ";
		String java = "Java";
		String cursoJava = curso + java; // concatenando duas varíaveis do tipo string

        String resultado2Com2 = "Resultado 2+2 = " + (2+2);
		System.out.println(resultado2Com2); // concatenando valores do tipo string e do tipo inteiro, porém nesse caso, como o 2+2 está entre parentêsis, ele irá imprimir 4.

		String resultado2Com2_ = "Resultado 2+2 = " + 2 + 2;
		System.out.println(resultado2Com2_); // concatenando valores do tipo string e do tipo inteiro.
```
Podemos utilizar o método `valueOf` para transformar um tipo em String.
```

        String um = String.valueOf(1); // utilizando o método valueOf para transformar o número 1 em uma String com conteúdo 1.
		System.out.println(um);
```
Podemos concatenar utilizando o operador de incremento `+=`.
```
        String concatenacao2 = "Lorem ipsum dolor sit amet, consectetur adipiscing elit, ";
		concatenacao2 += "sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad ";
		concatenacao2 += "minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea ";
		concatenacao2 += "commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit ";
		concatenacao2 += "essecillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat ";
		concatenacao2 += "non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.";
	
		System.err.println(concatenacao2);
```
Ao mudar uma string nós não estamos mudando a string original, nós estamos criando uma outra nova string, e assim sempre que essa string muda. As string são imutáveis, portanto, sempre que mudamos uma string, a string antiga vira lixo para ser varrido pelo garbage collector, por isso, fazer concatenação de strings dessa maneira não é uma boa prática, pois afeta diretamente a performance do código.

### Extraindo characters de uma String

Podemos fazer a extração de characters de uma string, até porque uma string é um array de characters. Para isso, podemos utilizar o método `charAt()`, que recebe o número do character que será extraído.
```
        String java = "Java";

		for (int i=0; i<java.length(); i++){
			System.out.println(java.charAt(i));
		}
```
Podemos também utilizar o método `getChars`, que transforma uma String em um array de caracteres.
```
		char[] jav = new char[3];
		java.getChars(0, 3, jav, 0); // ele recebe quatro parâmetros: indice do caracter inicial, indice do caracter final não inclusivo ou seja nesse caso não entra o 3, seguido do array que irá receber, e o indice inicial que receberá os dados nesse array.
		System.err.println(jav);

//o método getChars faz o mesmo que o código abaixo:
		for (int i=0, j=0; i<3; i++, j++){
			jav[j] = java.charAt(i);
		}
		System.out.println(jav);
```
Podemos fazer o mesmo com um array de bytes, utilizando o `getBytes`
```
		byte[] javBytes = new byte[3];
		java.getBytes(0, 3, javBytes, 0);
		System.out.println(Arrays.toString(javBytes));	
```
Podemos também utilizar o método `.toCharArray`, que transforma uma string em um array de chars.
```
	    String java = "Java";

    	char[] javaChars = java.toCharArray();
		System.out.println(javaChars);
```

### Comparação de Strings
Podemos fazer a comparação de strings com os métodos `equals` e `equalsIgonoreCase`, que retorna um boolean, ou seja, true ou false.
```
        String ola = "Olá";
		String ola2 = "OLÁ";
		String ola3 = "Olá";
		
		System.out.println(ola.equals(ola2)); //false, pois o método equals não ignora o maiusculo ou minúsculo, ou seja, as strings são diferentes frente à esse critério
		System.out.println(ola.equals(ola3)); //true, pois o método equals não ignora o maiusculo ou minúsculo, ou seja, as strings são diferentes frente à esse critério

        System.out.println("ola equals ola2 = " + ola.equalsIgnoreCase(ola2)); //true, pois o método equalsIgnoraCase ignora se é maísculo ou minúsculo
```
Podemos utilizar o operador do java `==`, porém esse operador compara exatamente o conteúdo do espaço da memória referenciada de cada varíavel, ou seja, ele compara referências e não o conteúdo. Quando criamos uma string pela atribuição simples, strings com conteúdos iguais estão no mesmo espaço de memória. A maneira mais segura para comparar strings é utilizando os métodos equals e equalsIgnoreCase, não o operador ==.
```
		String ola = "Olá";
		String ola2 = "OLÁ";
		String ola3 = "Olá";

        System.out.println("ola == ola1 " + (ola == ola2)); //false
		System.out.println("ola == ola3 " + (ola == ola3)); //true
```
Podemos também comparar regiões de strings, utilizando o `regionMatches`.
```

		String banana = "banana";
		String ana = "ana";
		String ban = "ban";
		
		
		System.out.println(banana.regionMatches(1, ana, 0, 3)); // o método recebe 4 parâmetros: indice inicial, a string que será comparada, o indice inicial da string que será comparada, a quantidade de strings que serão comparadas das duas. Nesse caso está comparando "ana" com "ana", ou seja, true.

        System.out.println(banana.regionMatches(2, ana, 1, 2)); // Nesse caso está comparando "na" com "na", ou seja, true.

		System.out.println(banana.regionMatches(true, 0, ban, 0, 3)); // Podemos também criar utilizar esse método com um parâmetros a mais, que é o ignoreCase, que é o primeiro parâmetro que colocamos true para ignorar e false para não ignorar. Nesse caso está comparando "ban" com "Ban" com o ignoreCase, ou seja, true.
```
Podemos também verificar se uma string começa ou termina com determinado caracter(es) utilizando os métodos `startWith` e `endsWith`, que retorna um booleano.
```
		System.out.println(banana.endsWith(ana)); // verifica se banana começa com ana, ou seja, é false
		System.out.println(banana.startsWith(ban)); // verifica se banana começa com ban, ou seja, é true.
```
Podemos o método `compareTo`, que retorna 3 opções, se é maior, menor ou igual. -1 para quando o primeiro objeto é maior que o segundo, 0 para o primeiro igual o segundo, e 1 ou mais para quando o primeiro é menor que o segundo. É muito utilizado para fazer ordenação de collections, por comparar quem é menor ou maior, podendo ser inserido em uma lógica para ordenar.
```
// nesse caso compara-se o número referente de cada caracter na tabela ASCII

		String a = "a";
		String b = "b";
		String aMaiusculo = "A";
		
		System.out.println(a.compareTo(b)); // -1
		System.out.println(b.compareTo(a)); // 1
		System.out.println(a.compareTo("a")); // 0
		System.out.println(a.compareTo(aMaiusculo)); // 32, pois o Maiusculo fica 32 posições na frente na tabela ASCII
		
		//-1 quando a > b
		//0 quando a == b
		//1 ou >1 quando a<b
```
Esse método é muito utilizada na interface comparable para ordenar, por exemplo, ArrayList.

### Buscas dentro de uma String
Podemos fazer buscas em strings utilizando os métodos `indexOf`, `lastIndexOf` e `contains`.<br>
O método indexOf procura um caracter(es) na string e retorna se encontrou ou não. Caso encontre, ele retorna o indice em que o caracter aparece a primeira vez na String. Caso não encontre, ele retorna -1.
```
        String banana = "banana";
		String ana = "ana";

		System.out.println(banana.indexOf('x')); // -1, pois não tem x em banana
		System.out.println(banana.indexOf('b')); //  0, pois é o indice da primeira vez que aparece b em banana
		System.out.println(banana.indexOf('a')); //  1, pois é o indice da primeira vez que aparece a em banana

        System.out.println(banana.indexOf(ana)); //  1, pois é o indice incial da primeira vez que aparece ana em banana
```
Para procurar última vez que um caractere(es) aparece em uma string.
```
		String banana = "banana";
		String ana = "ana";

		System.out.println(banana.lastIndexOf('a')); // 5, pois é o indice da última vez que aparece a em banana 
		System.out.println(banana.lastIndexOf(ana)); // 3, pois é o indice incial da última vez que aparece ana em banana
```
O método contains retorna um booleano para encontrado ou não.
```
		String banana = "banana";
		String ana = "ana";

		System.out.println(banana.contains(ana)); // true, pois banana contém ana
		System.out.println(banana.contains("ceu")); // false, pois banana não contém ceu
```

### Modificando uma String

Para modificar ou extrair uma parte de uma string podemos usar os métodos `substring`, `concat`, `replace` e `trim`. Esses métodos são muito utilizados para integrações de sistemas.<br>
O método substring pega uma parte da string a partir dos parâmetros passados, porém é apenas informativo, não recorta.
```
		String teste = "Isso é um teste.";
		
		System.out.println(teste.substring(10)); // "teste.", pois informa à partir do índice 10, indice inicial inclusivo
		System.out.println(teste.substring(10, 15)); // "teste", pois informa à partir do índice 10, indice inicial inclusivo, até o 15, indicial final não inclusivo
```
O método concat faz concatenação de strings. Pouco utilizado.
```
		String ola = "olá";
		String mundo = " mundo";
		String olaMundo = ola.concat(mundo); //ola + mundo
		System.out.println(olaMundo);
```
O método replace substitui um caracter(es) por um novo.
```
		String espacos = "i s p a ç o";
		String semEspacos = espacos.replace('i', 'e'); //troca o primeiro i por e
		System.out.println(semEspacos);
```
O método replaceAll substitui todos os caracteres por outros.
```
		semEspacos = semEspacos.replaceAll(" ", ""); // aqui podemos passar os RegEx. Nesse caso estamos trocando os espaços por uma string vazia, ou seja, estamos tirando os espaços.
```
O método trim recorta os espaços no final e no começo, semelhante à função ARRUMAR do Excel.
```
		String nome = " meu nome é: ";
		System.out.println(nome.trim());
```
Esses métodos são muito utilizados para conversar entre sistemas, utilizando arquivos, no caso os flat files, que seriam ou arquivos .xmls, .csv ou .txt.<br>
Algumas formas de fazer esses arquivos são:
- separadores, como o ponto e vírgula
- tamanhos de caracteres, por exemplo, de 0 à 5 é uma informação, de 6 à 10 é outra.
As manipulações são feitas através desses métodos acima, para lermos os dados corretamente.

### Transformar em Maiscula ou Minuscula
Podemos transformar todos os caracteres de uma string em maíuscula ou minúscula através dos métodos `.toUpperCase` e `.toLowerCase`. Muito utilizados em transformações de tudo em caixa alta, para poder fazer tranquilamente lógicas, comparações, etc.
```
        String teste = "Teste";
		
		String testeMinusc = teste.toLowerCase();
		String testeMaisc = teste.toUpperCase();

		System.out.println(testeMinusc);
		System.out.println(testeMaisc);
		
		// MUITO UTILIZADA PARA FAZER BOAS COMPARAÇÕES, MAIS SEGURAS: if (teste.toLowerCase().equals(teste.toLowerCase()))
```

### Juntar e Separar Strings

Podemos juntas e separar strings com os métodos `join` e `split`.
```
		String alfabeto = String.join(", ", "A", "B", "C", "D"); // o método join recebe parâmetros do tipo varargs, podendo passar quantas quantidades quisermos. O primeiro parâmetro é o separador, o juntador, e os parâmetros da frente são os parâmetros que serão juntados.
		System.out.println(alfabeto); // A, B, C, D

		String[] letras = alfabeto.split(", "); // o método split separa e cria um vetor ignorando o parâmetro passado.
		for (String letra : letras){
			System.out.println(letra); // ABCD
		}
		
		String doArquivo = "1;Antônio;30;";
		String[] infos = doArquivo.split(";"); // Muito utilizado para ler arquivos flat files que são separados por separadores.
		for (String info : infos){
			System.out.println(info);
            // resultado: 1
                          Antonio
                          30
		}
```

### Concatenar varias Strings - Melhor forma

A melhor forma de concatenar varias string é utilizando os métodos `StringBuffer` e `StringBuffer`.

O método StringBuffer faz a concatenação sem gerar lixo. Ele tem vários métodos que podem ser utilizados juntos. O StringBuffer é thread safe, ou seja, é mais recomendado ao trabalhar aonde estamos trabalhando com mais de um thread.
```
		String[] letras = {"B", "C", "D", "E", "F"};

		StringBuffer sb = new StringBuffer();
		for (String letra : letras){
			sb.append(letra); // o append faz a adição em um String, nesse caso devido ao for, todos os itens do array letras
		}
		alfabeto = sb.toString(); // chama o método toString para ter uma string única

        System.out.println(sb.reverse()); // o método reverse cria a string ao contrário
```
O método StringBuilder tem o mesmo funcionamento, mas sem o thread safe.
```
		StringBuilder sb_ = new StringBuilder();
		for (String letra : letras){
			sb_.append(letra);
		}
		alfabeto = sb_.toString();
		
		System.out.println(alfabeto);
```

### String Tokenizer

A classe String Tokenizer extrai informações de uma string e gera tokens.
```
		String doArquivo = "1;Antônio;30;";
		
		StringTokenizer st = new StringTokenizer(doArquivo, ";");       // o primeiro parâmetro e a string que será extraída as informações, e o segundo parâmetro é o delimitador.
		
		while (st.hasMoreTokens()){        // o método hasMoreTokens, ou seja, nesse caso, enquanto o StringTokenizer tem mais toquens
			System.out.println(st.nextToken());         // o método nextToken extraí o token
		}
```