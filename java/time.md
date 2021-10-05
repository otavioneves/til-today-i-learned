Lançado no Java 8, facilitou a manipulação de datas.
- LocalDate: é uma classe imutável para representar uma data. Seu formato padrão é yyyy-mm-dd;
```
import java.time.LocalDate;

public class Exemplo010 {
    public static void main(String[] args) {

        LocalDate hoje = LocalDate.now();

        System.out.println(hoje);
        // 2019-07-14

    }
}
```
Outro exemplo é manipular as datas:
```
        LocalDate hoje = LocalDate.now();

        LocalDate ontem = hoje.minusDays(1);

        System.out.println(hoje);
        // 2019-07-14

        System.out.println(ontem);
        // 2019-07-13
```
- LocalTime: é uma classe imutável para representar um padrão de hora-minuto-segundo. Utilização similar ao LocalDate;
```
import java.time.LocalTime;


public class Exemplo012 {
    public static void main(String[] args) {

        LocalTime agora = LocalTime.now();

        System.out.println(agora);
        // 23:53:58.421

    }
}
```
Outro exemplo é manipular o tempo:
```
public static void main(String[] args) {

        LocalTime agora = LocalTime.now();

        System.out.println(agora);
        // 23:53:58.421

        LocalTime maisUmaHora = agora.plusHours(1);

        System.out.println(maisUmaHora);
        // 00:55:37.421

    }
```

- LocalDateTime: junção do Date e Time, com precisão de nanosegundos.
```
import java.time.LocalDateTime;

public class Exemplo014 {
    public static void main(String[] args) {

        LocalDateTime agora = LocalDateTime.now();

        System.out.println(agora);
        // 2019-07-15T00:02:16.076

        LocalDateTime futuro = agora.plusHours(1).plusDays(2).plusSeconds(12);

        System.out.println(futuro);
        // 2019-07-17T01:02:28.076

    }
}
```