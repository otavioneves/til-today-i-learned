O java.util.calendar é uma classe que provê metodos para converter data entre um instante específico através de campos específicos e retornando vários dados da data. Alguns métodos interessantes dessa classe são:
```
        Calendar hoje = Calendar.getInstance();

        Calendar hoje = Calendar.getInstance(); //singleton

	int ano = hoje.get(Calendar.YEAR);
	int mes = hoje.get(Calendar.MONTH);                             // em java, o mês de Janeiro começa com 0
	int dia = hoje.get(Calendar.DAY_OF_MONTH);
	int hora = hoje.get(Calendar.HOUR_OF_DAY);
	int minutos = hoje.get(Calendar.MINUTE);
	int segundos = hoje.get(Calendar.SECOND);

        System.out.printf("Hoje é : %02d/%02d/%d %02d:%02d:%02d", dia, (mes+1), ano, hora, minutos, segundos);
```
Podemos manipular datas da seguinte forma:
```
        Calendar agora = Calendar.getInstance();

        System.out.println("A data corrente é : " + agora.getTime());   // A data corrente é : Sun Jul 14 20:50:31 BRT 2019

        agora.add(Calendar.DATE, -15);
        System.out.println("15 dias atrás: " + agora.getTime());        // 15 dias atrás: Sat Jun 29 20:50:31 BRT 2019

        agora.add(Calendar.MONTH, 4);
        System.out.println("4 meses depois: " + agora.getTime());       // 4 meses depois: Tue Oct 29 20:50:31 BRT 2019

        agora.add(Calendar.YEAR, 2);
        System.out.println("2 anos depois: " + agora.getTime());        // 2 anos depois: Fri Oct 29 20:50:31 BRT 2021
```