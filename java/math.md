O Java não é uma linguagem muito confiável para fazer cálculos com números, porém temos a classe math possui muitos métodos, como os abaixo:
### FUNÇÕES TRIGONOMÉTRICAS
- sin(x) = seno, recebe um ângulo em radianos (double) e retorna seu valor;
- cos(x) = cosseno, recebe um ângulo em radianos (double) e retorna seu valor;
- tag(x) = tangente, recebe um ângulo em radianos (double) e retorna seu valor;
- asin(x) = seno-1, recebe um valor (double) e retorna o angulo correspondente em radianos;
- acos(x) = cosseno-1, recebe um valor (double) e retorna o angulo correspondente em radianos;
- atag(x) = tangente-1, recebe um valor (double) e retorna o angulo correspondente em radianos;
- toRadians(x) = converte um grau em radiano;
- toDegrees(x) = converte um radiano em grau.

### FUNÇÕES EXPONENCIAIS
- pow(x,y) = potência de x elevado à y;
- sqrt(x) = raiz quadrada de x;
- cbrt(x) = raiz cúbica de x;
- exp(x) = exponencial de x;
- log(x) = logaritmo na base 2 de x;
- log10(x) = logaritmo na base 10 de x;
- scalb(x,y) = fator.

### FUNÇÕES DE ARRENDONDAMENTO
- abs(x) = número absoluto de x;
- ceil(x) = menor número inteiro maior ou igual a x (arredonda pra cima);
- floor(x) = menor número inteiro menor ou igual a x (arredonda pra baixo);
- floorDiv(x,y) = menor número inteiro menor ou igual o quociente de x por y;
- floorMod(x,y) = menor número inteiro menor ou igual ao resto de x por y;
- round(x) = arredonda x;
- max(x,y) = retorna o maior número, x ou y;
- min(x,y) = retorna o menor número, x ou y;
- nextAfter(x,y) = próximo número depois de x em direção ao y;
- nextDown(x) = próximo número inteiro antes de x;
- nextUp(x) = próximo número inteiro depois de x.

### OUTRAS FUNÇÕES
- addExact(x,y) = soma y em x;
- subtractExact(x,y) = subtrai y de x;
- multiplyExact(x,y) = multiplica x por y;
- incrementExact(x) = incrementa 1 em x;
- decrementExact(x) = decrementa 1 em x;
- random() = gera número aleatórios.

```
        System.out.println(Math.pow(2, 3)); // raiz quadrada
		
		System.out.println(Math.round(4.7));
		
		System.out.println(Math.round(4.4));
		
		System.out.println(Math.ceil(4.4));
		
		System.out.println(Math.ceil(4.7));
		
		System.out.println(Math.floor(4.4));
		
		System.out.println(Math.floor(4.7));
		
		System.out.println(Math.round(Math.random() * 100)); //gera um número de 0 à 1. Se quisermos um número de 0 à 100, multiplicamos por 100 esse resultado, depois de arrendondar.
		
		System.out.println(Math.sin(Math.toRadians(30)));
		
		System.out.println(Math.cos(Math.toRadians(1)));
		
		System.out.println(Math.tan(Math.toRadians(45)));
```
Além da Classe Math, a maneira correta de manipular números com maior segurança, utilizamos as classes BigNumber e BigDecimal