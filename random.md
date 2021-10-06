Podemos utilizar a classe Random para gerar números aleatórios. A classe Math também tem métodos randoms.
```
		System.out.println(Math.floor(Math.random() * 100));        // o Math.random gera números de 0 à 1, nesse caso, multiplicando por 100 e arredondando, arrendondamos
```
Utilizando a classe Random:
```
		Random aleatorio = new Random();
		
		System.out.println(aleatorio.nextInt());        // pegando um número aleatório que será um inteiro
		
        System.out.println(aleatorio.nextInt(100));        // pegando um número aleatório que será um inteiro de 0 à 99, o 100 não é incluído

		System.out.println(aleatorio.nextInt(5));   // pegando um número aleatório que será um inteiro de 0 à 4, o 5 não é incluído
```