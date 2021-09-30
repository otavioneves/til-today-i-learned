O printf serve para imprimir de uma maneira formatada:
- `System.out.printf(format, varargs)`
- %s = utilizado para informar que o parâmetro posterior é em formato de string;
```
		System.out.printf("%s", "Olá, Mundo!");
```
- %S = utilizado para informar que o parâmetro posterior é em formato de string e formata tudo para caixa alta;
```
		System.out.printf("%S", "Olá, Mundo!");
```
- %c e %C = utilizado para informar que o parâmetro posterior é um caracter, e formata em caixa alta ao usar o C maiusculo;
```
		System.out.printf("%c", 'c');
		System.out.printf("%C", 'c');
```
- %n = utilizado para pulara linha;
- %d = utilizado para informar que o parâmetro posterior é um número inteiro;
```
int valor = 123456789;
System.out.printf("%d", valor);
```
- %f = utilizado para informar que o parâmetro posterior é um número de ponto flutuante;
```
		double pontoFlutuante = 3.1456789;
		System.out.printf("%f", pontoFlutuante);
```
- número entre o % e o s: padroniza o número de caracteres com alinhamento à direita;
```
		String olaMundo = "Olá, Mundo!";
		System.out.printf("%20s", olaMundo);
```
- sinal de menos, seguido do número entre o % e o s: padroniza o número de caracteres com alinhamento à esquerda;
```
		String olaMundo = "Olá, Mundo!";
		System.out.printf("%-20s", olaMundo);
```
- sinal de mais, seguido do d ou do f: mostra o sinal do número, tanto mais quanto menos;
```
		int valor = -123456789;
		System.out.printf("%+d", valor);
```
- número 0 e número de caracteres entre o % e o s: padroniza o número de caracteres com alinhamento à direita e completa o restante com 0;
```
		String olaMundo = "Olá, Mundo!";
		System.out.printf("%020s", olaMundo);
```
- ponto ou vírgula entre o % e o d: formata com a marcação de milhares;
```
        System.out.printf("%,d", valor);
```
- espaço entre o % e o d: formata o número para que caso seja negativo, ele imprime o menos, caso seja positivo, ele imprime um espaço;
```
    	int valor = 123456789;
        int valor2 = -123456789;
		System.out.printf("% d", valor2);

		System.out.printf("% d", valor);
```
- ponto seguido de número entre o % e o f: formata a quantidade de números após a vírgula em números de pontos flutuantes e arredonda;
```
		System.out.printf("%.3f", pontoFlutuante);
```
- para formatar no valor monetário:
```
		System.out.printf("R$%10.2f", pontoFlutuante);
```

### Teste completo:
```
    private static void testeMaisCompleto(){
		
		double[] precos = {10000, 123.54, 7843.567, 1, 4.56789};
		
		for (int i=0; i<precos.length; i++){
			System.out.printf("%s %02d: total de R$%,10.2f%n", "Item", i+1, precos[i]);
		}
		
		//Java.util.Formater
	}
```