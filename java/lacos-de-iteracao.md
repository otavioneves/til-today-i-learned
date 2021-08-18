Os lações de iteração são o `for` e o `while`.
- for: a estrutura básica do for é formada inicialmente por uma expressão inicial, uma expressão de verificação de continuidade  e a última expressão de ação que irá acontecer à cada volta;
```
    for(int i = 0; i < 5; i++ ) //iniciando com o contador (i) em 0, repetir o laço enquanto o i for menor que 5, e à cada laço incrementar 1 em i.
```
Dentro do laço for podemos usar o comando `break`, dentro de um if, para pararmos o for devido à alguma condição.<br>
Também podemos usar o comando `continue`, dentro de um if, para não realizar o laço devido à alguma condição.<br>
Exemplo:


- while: a estrutura básica do while é formada por uma expressão condicional, e dentro do laço é feito o incremento.
```
        int i = 0;
		while (i < 10) {
			i++;
		}
```
<br>
O laço for é mais para quando você tem uma quantidade de iterações conhecidas, mesmo que for através de uma varíavel. Já o while é mais utilizada para ser utilizado devido à uma condição.<br>
Dentro do while também tem a vantagem de poder utilizar uma varíavel já presente no código.<br>
Os comandos break e continue também são válidos para o while.<br>
Exemplo:
```
//break
        int i = 0;
		while (i < 10) {
			if (i == 5) {
				System.out.println("Vai parar!");
				break;
			}
			System.out.println(i + ": Um texto qualquer.");
			i++;
		}

//continue
		int i = 0;
		while (i < 10) {
			if (i == 5) {
				System.out.println("Vai continuar...");
				i++;
				continue;
			}
			
			System.out.println(i + ": Um texto qualquer.");
			i++;
		}
```