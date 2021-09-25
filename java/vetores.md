Vetores, ou arrays, são variáveis que podem guardar mais de um valor.<br>

A sintaxe de um vetor de 1 dimensão é a seguinte:
```
String[] cardapio = new String[] { "Calabresa", "Atum", "Queijo", "Presunto"};
```
Para usarmos no código o tamanho do vetor, utilizamos a varíavel seguida de `.length`
```
        for(int i = 0; i < cardapio.length; i++) { // repete o laço enquanto i é menor que o tamanho do vetor
		    System.out.println("[" + i + "] " + cardapio[i]); // escreve i seguido do conteúdo de cada posição definida por i
		}
```
As posições (índices) em um vetor começam com 0, e vão aumentando de 1 em 1: 0, 1, 2, 3, 4, 5...

Quando não é colocado os itens diretamente do vetor, podemos definir apenas o tamanho do array, conforme abaixo:

```
        String[] cardapio = new String[4];
		cardapio[0] = "Calabresa";
		cardapio[1] = "Atum";
		cardapio[2] = "Queijo";
		cardapio[3] = "Presunto";
```

Os vetores podem também ser de duas dimensões, podendo guardar valor em X e em Y, semelhantes à uma matriz. Cada dimensão de um vetor de duas dimensões precisa ser um vetor de 1 dimensão, ou seja, a sintaxe de um vetor de 2 dimensões é guardar não valores nos seus índices, mas sim vetores de 1 dimensão, conforme exemplo abaixo:
```
        Double[] faturamentoJaneiro = new Double[] { 1500.0, 2000.0, 1700.0 };
		Double[] faturamentoFeveriro = new Double[] { 1000.0, 2500.0, 1800.0 };
		
		Double[][] faturamentoAnual = new Double[][] { faturamentoJaneiro, faturamentoFeveriro };
```
As posições (índices) em um vetor começam com 00, e vão aumentando de 1 em 1 nas linhas e começando com 0 e vão aumentando de 1 em 1 nas colunas.
O Primeiro colchete é a linha e o segundo a coluna:
- //[00][01][02]
- //[10][11][12]
- //[20][21][22]

Como no exemplo abaixo, para acessar cada indíce do vetor de duas dimensões usamos dois for, o primeiro irá acessar a linha, travando no número da linha, e o segundo vai percorrer todo o tamanho do vetor de 1 dimensão dessa linha, ou seja, as colunas (0,1,2,3,...). Enquanto a linha está travada pelo primeiro for, o segundo for executa quantas vezes for o tamanho do vetor de 1 dimensão. Depois de acabar esse vetor, o primeiro for altera de linha e o segundo for vai percorrer esse outro vetor de 1 dimensão.
```
            for (int i = 0; i < faturamentoAnual.length; i++) {
			System.out.println("Mês: " + (i + 1));
			
			Double[] mes = faturamentoAnual[i];
			
			for(int y = 0; y < mes.length; y++) {
				Double dia = mes[y];
				
				System.out.println("Dia " + (y + 1) + ": " + dia);
			}
		}
```
Outra forma é acessar diretamente variando, nesse caso i e y, e acessando os índices. Ou seja, ao ínves de utilizar um vetor para ir guardando as informações, utiliza-se cada linha e percorre-se a coluna do vetor original.
```
        for (int i = 0; i < faturamentoAnual.length; i++) {
			    System.out.println("Mês: " + (i + 1));
			
			    for(int y = 0; y < faturamentoAnual[i].length; y++) {
				    System.out.println("Dia " + (y + 1) + ": " + faturamentoAnual[i][y]);
			    }
		}
```
<br>
Outra forma de executar o for em arrays é a seguinte:
<br>

```
	public class Arrays {

	public static void main(String[] args) {
		
		double[] temperaturas = new double[365];
		temperaturas[0] = 31.3;
		temperaturas[1] = 32;
		temperaturas[2] = 33.7;
		temperaturas[3] = 34;
		temperaturas[4] = 33.1;

		for (double temp : temperaturas){
			System.out.println(temp);
		}
	}
	}
```
<br>
FUNCIONALIDADES
- .length = retorna o tamanho do vetor:

```
		int[] vetorA = new int[5];
		
		for (int i=0;i<vetorA.length;i++) {
			System.out.print("Digite o " + (i+1)+"º número: ");
			
		}
```

Para ja settar algum dado no momento da criação de um array ou matriz, podemos utilizar as chaves, conforme abaixo:

```
double[] notasAluno1= {7,8,9,10};
```

```
double[][] notasAlunos= {{7,8,9,10},{8,6,7,10}};
```

- Arrays Irregulares: matriz de vetores de tamanhos diferentes:

```
		String[][] nomesFilhos = new String[numEntrevistados][];
		
		for (int i=0; i<nomesFilhos.length; i++){
			
			System.out.println("Entre com a quantidade de filhos");
			int qtdFilhos = scan.nextInt();
			
			nomesFilhos[i] = new String[qtdFilhos];
			
			for (int j=0; j<nomesFilhos[i].length; j++){
				
				System.out.println("Digite o nome do filho " + (j+1));
				
				nomesFilhos[i][j] = scan.next();
			}
		}

```