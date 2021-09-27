Os wrapper são as classes que representam os tipos primitivos no Java. As classes impacotam os tipos promitivos.
As classes podem ser instanciadas, tem o seu próprio construtor.
```
		short num1 = 1;
		byte num2 = 10;
		int num3 = 100;
		long num4 = 10000l;
		float num5 = 3.5f;
		double num6 = 3.55555;
		boolean flag = true;
		char a = 'a';
		
        // Classes Wrappers
		Short num7 = new Short((short) 1);
		Byte num8 = new Byte((byte)10);
		Integer num9 = new Integer(100);
		Long num10 = new Long(10000l);
		Float num11 = new Float(3.5f);
		Double num12 = new Double(3.5555);
		Boolean flag2 = new Boolean(true);
		Character b = new Character('b');
```
Todas as classes wrappers podem ser convertidas para outros tipos através do métodos value, valueOf ou parse.
```
		Integer num13 = new Integer("100"); //NumberFormatException
		
		Double num14 = new Double("3.5"); //3,5 para quem usar PC Português Brasil
		
		System.out.println(num13.intValue());
		System.out.println(num13.longValue());
		
		Long num15 = num13.longValue();
		
		int num16 = Integer.parseInt("100000"); // pode disparar uma exception NumberFormatException caso a String não for um número int.
		
		double num17 = Double.parseDouble("3.555"); //pode disparar uma exception NumberFormatException caso a String não for um número double.
		System.out.println(num17);
		
		Integer num18 = Integer.valueOf(1343);// transforma um número inteiro em uma instância da Classe Integer.
		System.out.println(num18);
		
		System.out.println(num9 == num13); //== não funciona com wrappers - false
```
O operador `==` não funciona com wrappers. Para fazer comparação utilizamos o método `.equals()`.
Os processos de Autoboxing e Auto-unboxing são processos aonde transformamos tipos primitivos (int, double, char, float, etc) em objetos.
- Autoboxing: pegar o tipo promitivo e colocar em uma caixa.

```
//autoboxing
		Short num7 = 1;
		Byte num8 = 10;
		Integer num9 = 100;
		Long num10 = 100l; //new Long(10000l);
		Float num11 = 3.5f; //new Float(3.5f);
		Double num12 = 2.55555;
		Boolean flag2 = true;
		Character b_ = 'b';
```

= Auto-unboxing: pegar um tipo primitivo e receber um wrapper, transformando um wrapper em um tipo primitivo:

```
		//auto un-boxing
		int num13 = num9;       // mesma coisa que num9.intValue();
```
