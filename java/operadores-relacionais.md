Os operadores relacionais são operadores responsáveis por executar relações entre dois itens.
- == : igual a
- != : diferente de
- > : maior que
- < : menor que
- >= : maior ou igual a
- <= : menor ou igual a

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
```

- .equals() : verifica se um é igual ao outro.
- .equalIgnoreCase : verifica se um é igual ao outro ignorando maiúscula ou minúscula.