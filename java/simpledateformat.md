A classe SimpleDateFormat é utilizada para formatarmos data.
```
        SimpleDateFormat sdf = new SimpleDateFormat("dd-MMM-yyyy hh:mm:ss a z");            // criando uma instância da classe com a formatação digitada: "dd-MMM-yyyy hh:mm:ss a z"
		
		Calendar data = new GregorianCalendar(2010, 5, 4, 14, 32, 25);						// definindo uma instânca da classe Gregorian Calendar, definindo seus valores
		
		System.out.println(sdf.format(data.getTime()));										// utilizando o getTime para termos a data
```


```
		SimpleDateFormat sdf1 = new SimpleDateFormat("dd/MM/yyyy");
		String minhaData = "20/02/2000";

		Date minhaDataEmDate = sdf1.parse(minhaData);										// transformando uma String para Date
			
		System.out.println(minhaDataEmDate);
			
		System.out.println(sdf.format(minhaDataEmDate));
```
O DateFormat é mais recomendado para trabalhar com o locale da aplicação, já o SimpleDateFormat é quando queremos especificar o formato da data.