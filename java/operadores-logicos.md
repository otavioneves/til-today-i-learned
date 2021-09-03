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
- ! : operador not
- `variavelbooleana ? açãotrue : ação false` : operador ternário, é se caso e a varíavel for true, executa a primeira ação, caso for ação, executa a segunda ação.