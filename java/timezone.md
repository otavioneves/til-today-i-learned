A classe timezone é utilizada para padronizar as informações de horários, principalmente em relação as diferentes horas ao redor do mundo.
```
		Calendar calendar = Calendar.getInstance();
		TimeZone tz = calendar.getTimeZone();           // pega o seu time zone
		
		System.out.println(tz);
```
Para ver todos os fusos horários do mundo utilizamos:
```
		String[] fusos = TimeZone.getAvailableIDs();
		for (String fuso: fusos) {
			System.out.println(fuso);
		}
```
Para configurar um fuso horário padrão ou apenas fazer uma alteração no fuso horário:
```
		TimeZone tzSP = TimeZone.getTimeZone("America/Sao_Paulo");
		
		System.out.println(tzSP.getDisplayName());          // retorna o horário padrão
		System.out.println(tzSP.getID());                   // retorna o id
```
Podemos utilizar o timezone para converter datas. No caso abaixo vamos converter qualquer horário e fuso para o horário e fuso do Brasil:
```
		Calendar agora = Calendar.getInstance();
		SimpleDateFormat sdf = new SimpleDateFormat("dd-MMM-yyyy hh:mm:ss a z");
		System.out.println(sdf.format(agora.getTime()));
		
		Calendar agoraSP = Calendar.getInstance(tzSP);
		System.out.println(agoraSP.getTimeZone());
		System.out.println(sdf.format(agoraSP.getTime()));

        agoraSP.add(Calendar.HOUR_OF_DAY, tzSP.getOffset((System.currentTimeMillis())) / 1000 / 60/ 60);
		System.out.println(sdf.format(agoraSP.getTime()));
```