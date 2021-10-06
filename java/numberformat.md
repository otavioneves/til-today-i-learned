A classe NumberFormat é utilizada para formatar número sem tanta precisão decimal. No caso de trabalhar com moedas, é mais recomendada a classe NumberDecimal. A classe segue a formatação de cada local que será utilizado o código, podendo ser configurada dependendo da aplicação.

```
		Locale en = new Locale("en", "United States");          // settando o locale
		NumberFormat nf = NumberFormat.getInstance(en);         // pegando o NumberFormat em relação ao locale criado

		String num = nf.format(100.99);         // utilizando a formatação com o .format
		System.out.println(num);
```
Podemos fazer também com outro locale, no caso abaixo é o pt BR.
```
		Locale br = new Locale("pt", "Brazil");
		nf = NumberFormat.getInstance(br);

		num = nf.format(100.99);
		System.out.println(num);
```
Podemos também trabalhar com valores de moeda, também utilizando o locale.
```
		NumberFormat moeda = NumberFormat.getCurrencyInstance(Locale.getDefault());
		
		String valor = moeda.format(100.99);            // formata também o símbolo da moeda
		System.out.println(valor);

        Currency currency = moeda.getCurrency();        // a classe Currency
		System.out.println(currency);
```
Podemos também trabalhar com porcentagem, também utilizando o locale.
```
		NumberFormat porcent = NumberFormat.getPercentInstance();
		String porcentagem = porcent.format(99.987);            // transforma o número em porcentagem
		System.out.println(porcentagem);
```
Podemos também formatar a quantidade de casas decimais e inteiras.
```		
		porcent.setMaximumIntegerDigits(7);         // setta o máximo de casas inteiras
		porcent.setMinimumIntegerDigits(5);         // setta o mínimo de casas inteiras
		
		porcent.setMaximumFractionDigits(2);        // setta o máximo de casas decimais
		porcent.setMinimumFractionDigits(1);        // setta o mínimo de casas decimais
		
		porcentagem = porcent.format(99.987);
		System.out.println(porcentagem);
```
Podemos também fazer arrendondamentos.
```
		nf = NumberFormat.getInstance(Locale.getDefault());
		
		nf.setRoundingMode(RoundingMode.UP);        // o após o RoundindMode é a maneira arredonda
		nf.setMaximumFractionDigits(0);             // settando o máximo de digitos fracionários
		nf.setMinimumFractionDigits(0);             // settando o mínimo de digitos fracionários
		System.out.println(nf.format(99.50));
```
Podemos fazer também um parse do Number Format.
```
		Number num3 = nf.parse("100.00");
		System.out.println(num3.intValue())
```