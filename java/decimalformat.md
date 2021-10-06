A classe DecimalFormat é mais utilizada para quando se precisa de mais precisão ou mais controle da formatação. A classe DecimalFormat extende a NumberFormat, ou seja, tudo que a NumberFormat faz a DecimalFormat também faz.
```
		String padrao = "###.###,##";                   // utilizamos as # para definir a quantidade de números entre os ponto e virgula como marcador e separador
		DecimalFormat df = new DecimalFormat(padrao);   // recebe a string do padrão, instancia passando o padrão
        
        System.out.println(df.format(1234567890.123));  // irá imprimir 1.234.567.890,123, conforme o padrão passado
```
Podemos também definir o padrão através do apllyPattern:
```
		df.applyPattern(padrao);
```
Podemos também trocar o locale, consequentemente em alguns casos, os separadores ou marcadores, dependendo do locale, e os dois tem que estar alinhados.
```
		DecimalFormatSymbols dfs = new DecimalFormatSymbols(new Locale("pt", "Brazil"));        // locale pt Br
		dfs.setDecimalSeparator(',');           // virgula para separar decimais
		dfs.setGroupingSeparator('.');          // ponto para separar os grupos de inteiros
```
Podemos criar vários padrões de acordo com o locale:
```
		String padrao2 = "###,###.##";          // padrão americano
		df = new DecimalFormat(padrao2, dfs);
		System.out.println(df.format(1234567890.123));
		
		String padrao3 = "###,###,###.##";      // padrão brasileiro
		df = new DecimalFormat(padrao3, dfs);
		df.setGroupingSize(4);           // configurando o tamanho do grupo, geralmente é a cada 3 número, nesse caso está settando de 4 em 4
		System.out.println(df.format(1234567890.123));
		
		String padrao4 = "\u00A4###,###,000.00%";   // configurando a formatação, mais informações na documentação, e é bem completa
		df = new DecimalFormat(padrao4, dfs);
		System.out.println(df.format(0.1));
```