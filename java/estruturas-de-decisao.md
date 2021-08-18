As estruturas de decisão são:
- if: (se)
- else: (senão)

Para utilizar o if encadeado utilizamos a estrutura `else if`:
```
        Boolean pesoLeve = (peso <= 60) && (peso > 0);
		Boolean pesoMedio = (peso > 60) && (peso <= 90);
		Boolean pesoPesado = peso > 90;
		
		if (pesoLeve) {
			System.out.println("O lutador(a) é peso leve.");
		} else if (pesoMedio) {
			System.out.println("O lutador(a) é peso médio.");
		} else if (pesoPesado) {
			System.out.println("O lutador(a) é peso pesado.");
		} else {
			System.out.println("O lutador(a) não se encaixa em categoria alguma.");
		}
```

Podemos fazer também da seguinte maneira, com um if dentro do else.
```
        Boolean pesoLeve = peso <= 60;
		Boolean pesoMedio = (peso > 60) && (peso <= 90);
		Boolean pesoPesado = peso > 90;
		
		if (pesoLeve) {
			System.out.println("O lutador(a) é peso leve.");
		} else {
			Boolean pesoMedio = (peso > 60) && (peso <= 90);
			
			if (pesoMedio) {
				System.out.println("O lutador(a) é peso médio.");
			} else {
				Boolean pesoPesado = peso > 90;
				
				if (pesoPesado) {
					System.out.println("O lutador(a) é peso pesado.");
				}				
			}
/		}
```

- switch: (caso) - Dentro do switch não pode ter uma varíavel Double como condição;
        switch(mes) {
		case 1: desconto = 0.0;
			break;
		case 2: desconto = 0.0; 
			break;
		case 3: desconto = 15.0; 
			break;
		case 4: desconto = 30.0; 
			break;
		case 5: desconto = 10.0; 
			break;
		case 6: desconto = 10.0; 
			break;
		case 7: desconto = 10.0; 
			break;
		case 8: desconto = 10.0; 
			break;
		case 9: desconto = 10.0; 
			break;
		case 10: desconto = 20.0; 
			break;
		case 11: desconto = 10.0; 
			break;
		case 12: desconto = 0.0;
			break;