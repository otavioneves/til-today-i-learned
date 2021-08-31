Os operadores lógicos são utilizados para tomar decisões.
```
        Boolean carrinhoMaiorQue100 = false;
		Boolean periodoDePromocao = true;
		Boolean jaFezCompraNaLoja = false;
		Boolean pagamentoAVista = true;
		
//		Boolean aplicarDesconto = carrinhoMaiorQue100 && periodoDePromocao; OPERADOR LÓGICO E
		
//		Boolean aplicarDesconto = carrinhoMaiorQue100 || periodoDePromocao; OPERADOR LÓGICO OU
		
		Boolean aplicarDesconto = periodoDePromocao && (carrinhoMaiorQue100 || jaFezCompraNaLoja) && pagamentoAVista; // Irá aplicar desconto se estiver dentro do período de promoção e, ou o carrinho esteja com mais de 100 reais ou o cliente ja tenha feita compra na loja, e o pagamento seja à vista.
		}
```
Os operadores lógicos são operadores quer fazem uma relação e retornam sempre um resultado booleano.

```
        Boolean tresMaiorQueDois = 3 > 2;
		
		Boolean tresMenorQueDois = 3 < 2;
				
		Boolean tresMaiorQueTres = 3 > 3;
			
		Boolean tresMaiorOuIgualATres = 3 >= 3;
				
		Boolean tresMenorOuIgualATres = 3 <= 3;
		
		Boolean doisIgualADois = 2 == 2; // Operador de igualdade, tem que usar dois sinais "=". Para variaveis do tipo normal, a comparação pode ser apenas de -127 à 128. Para numeros fora desse intervalo, tem que usar variaveis do tipo primitivo.
		
		Boolean doisDiferenteDeDois = 2 != 2; // Operador "diferente de";
```
Para comparar se variavéis são iguais utilizamos `variavel1.equals(variavel2)`.

```
        Boolean cincoIgualACinco = cinco.equals(cinco);