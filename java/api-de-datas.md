A partir do java 8 foi implementado uma api para se trabalhar com datas, ela é segura e é compatível com datas. LocalDate, LocalTime, LocalDateTime e ZoneId.
- Para trabalharmos com data usaremos o `LocalDate`, que é do padrão ISO: dd-MM-yyyy.
```
LocalDate agora = LocalDate.now();
System.out.println(agora);
```
Para transformar 3 informações de strings, ano, mês e dia, em uma varíavel do tipo local date podemos fazer de duas maneiras:
```
System.out.println(LocalDate.of(2019, 2, 1));           // maneira 1

System.out.println(LocalDate.parse("2020-02-01"));      // maneira 2, caso a string esteja no padrão ISO
```
Para adicionar ou diminuir dias, mês, semanas, mês e anos, com plus ou minus:
```
System.out.println(agora.plusDays(30));                 // nesse caso, somando 30 dias

System.out.println(agora.minus(1, ChronoUnit.MONTHS));  // nesse caso, voltando 1 mês através do enum ChronoUnit
```
Para obter o dia da semana, dia do mês, dia do ano, se o ano é bissexto:
```
System.out.println(agora.getDayOfWeek());
System.out.println(agora.getDayOfMonth());
System.out.println(agora.getDayOfYear());
System.out.println(agora.isLeapYear());
```
- Para trabalharmos com horário usaremos o `LocalTime`, que é do padrão ISO: horário militar.
```
LocalTime hAgora = LocalTime.now();
System.out.println(hAgora);
```
Assim como no Local date, podemos transformar strings em LocalTime.
```
System.out.println(LocalTime.of(20, 18));
System.out.println(LocalTime.parse("20:18"));
```
Podemos também somar e diminuir horas, minutos, segundo, etc.
```
System.out.println(hAgora.plusMinutes(50));                 // nesse caso, somando 50 minutos
System.out.println(hAgora.minus(40, ChronoUnit.MINUTES));   // nesse caso, diminuindo 40 minutos através do enum ChronoUnit
```
Para obter a hora, minuto, segundo, etc:
```
System.out.println(hAgora.getHour());                       // pegando a hora
```
- Para trabalharmos com os dois, utilizamos o `LocalDateTime`:
```
LocalDateTime agoraCompleto = LocalDateTime.now();
System.out.println(agoraCompleto);
```
Para transformar strings em LocalDateTime.
```
System.out.println(LocalDateTime.of(2019, 2, 16, 20, 25, 10));
System.out.println(LocalDateTime.parse("2019-02-16T20:25:10"));
```
Podemos adicionar horas, minutos, segundos, etc.
```
System.out.println(agoraCompleto.plusYears(20));
```
- Para obtermos o fuso horário, podemos usar o `ZoneId` e o `ZoneDateTime`:
```
ZoneId fuso = ZoneId.systemDefault();
System.out.println(fuso);
```
Para obter todas os fusos horários:
```
Set<String> fusos = ZoneId.getAvailableZoneIds();       // o set é uma lista de objetos que não se repetem
for (String f : fusos) {
	System.out.println(f);
}
ZoneId sp = ZoneId.of("America/Sao_Paulo");
```
Para transformar uma string em ZoneId e utilizar o ZoneDateTime:
```
ZoneId sp = ZoneId.of("America/Sao_Paulo");
ZonedDateTime zdt = ZonedDateTime.of(LocalDateTime.parse("2019-02-16T20:25:10"), sp);
System.out.println(zdt);
System.out.println(ZonedDateTime.parse("2019-02-16T20:25:10-02:00[America/Sao_Paulo]"));
```
Podemos também manipular o fuso horário:
```
ZoneOffset offset = ZoneOffset.of("+02:00");
OffsetDateTime offsetdt = OffsetDateTime.of(agoraCompleto, offset);
System.out.println(offsetdt);

Date date = new Date();
Calendar c = Calendar.getInstance();
LocalDateTime ldtDate = LocalDateTime.ofInstant(date.toInstant(), sp);
System.out.println(ldtDate);
System.out.println(LocalDateTime.ofInstant(c.toInstant(), sp));
```