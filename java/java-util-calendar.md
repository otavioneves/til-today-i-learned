O java.util.calendar é uma classe que provê metodos para converter data entre um instante específico através de campos específicos e retornando vários dados da data.
```
        public static void main(String[] args) {

        Calendar agora = Calendar.getInstance();

        System.out.println(agora);
```
Manipulando datas:
```
        public static void main(String[] args) {

        Calendar agora = Calendar.getInstance();

        System.out.println("A data corrente é : " + agora.getTime());
        // A data corrente é : Sun Jul 14 20:50:31 BRT 2019

        agora.add(Calendar.DATE, -15);
        System.out.println("15 dias atrás: " + agora.getTime());
        // 15 dias atrás: Sat Jun 29 20:50:31 BRT 2019

        agora.add(Calendar.MONTH, 4);
        System.out.println("4 meses depois: " + agora.getTime());
        // 4 meses depois: Tue Oct 29 20:50:31 BRT 2019

        agora.add(Calendar.YEAR, 2);
        System.out.println("2 anos depois: " + agora.getTime());
        // 2 anos depois: Fri Oct 29 20:50:31 BRT 2021

    }
```