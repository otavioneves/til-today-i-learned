O pacote java.util.Date é utilizado para trabalhar com datas no código. Atualmente trabalhar com a classe date não é melhor forma de se trabalhar com datas, porém, em alguns casos ainda é muito usado, como linhas de dados em bancos de dados.
- getTime() - retorna os milisegundos desde 1 de Janeiro de 1970
- getDate() - retorna o dia do mês (DEPRECATED)

### Construtores
- Date(): retorna informações de data padrão;
```
import java.util.Date;

public class Exemplo001 {

    public static void main(String[] args) {

        Date novaData = new Date();

        System.out.println(novaData);

    }

}
```
- Date(long date): retorna informações quando passamos informação no padrão EPOCH
```
    public static void main(String[] args) {

        Long currentTimeMillis = System.currentTimeMillis();

        System.out.println(currentTimeMillis);

        Date novaData = new Date(currentTimeMillis);

        System.out.println(novaData);

    }
```

### Métodos
- isAfter e isBefore: comparadores de datas com saída booleana;
```
        Date dataNoPassado = new Date(1513124807691L);

        Date dataNoFuturo = new Date(1613124807691L);

        // Comparando se a dataNoPassado é posterior a dataNoFuturo
        boolean isAfter = dataNoPassado.after(dataNoFuturo);

        System.out.println(isAfter);

        // Comparando se a dataNoPassado é anterior a dataNoFuturo
        boolean isBefore = dataNoPassado.before(dataNoFuturo);

        System.out.println(isBefore);
```
- compareTo e equals: comparadores de datas com saída booleana;
```
        public static void main(String[] args) {

        Date dataNoPassado = new Date(1513124807691L); //Tue Dec 12 22:26:47 BRST 2017

        Date dataNoFuturo = new Date(1613124807691L); //Fri Feb 12 08:13:27 BRST 2021

        Date mesmaDataNoFuturo = new Date(1613124807691L); //Fri Feb 12 08:13:27 BRST 2021

        /** Comparando se as datas são iguais */
        boolean isEquals = dataNoFuturo.equals(mesmaDataNoFuturo);

        System.out.println(isEquals); //true

        /** Comparando uma data com a outra */
        int compareCase1 = dataNoPassado.compareTo(dataNoFuturo); //passado -> futuro

        int compareCase2 = dataNoFuturo.compareTo(dataNoPassado); //futuro -> passado

        int compareCase3 = dataNoFuturo.compareTo(mesmaDataNoFuturo); //datas equivalentes

        System.out.println(compareCase1); // -1

        System.out.println(compareCase2); // 1

        System.out.println(compareCase3); // 0

    }
```
- toInstant: indicado para fazer marcações de datas;
```
import java.time.Instant;
        public static void main(String[] args) {

        Date dataInicio = new Date(1513124807691L);
        System.out.println(dataInicio);
        // Tue Dec 12 22:26:47 BRST 2017

        Instant instant = dataInicio.toInstant();
        System.out.println(instant);
        // 2017-12-13T00:26:47.691Z
    }

```
- from: 