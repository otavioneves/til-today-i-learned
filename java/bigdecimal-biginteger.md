Podemos usar as classes BigDecimal e BigInteger para fazer cálculos exatos de números decimais e números inteiros, muito importante para utilização em sistemas financeiros. As operações são feitas com métodos e os números são construídos através dos construtores. As duas classes não tem limite, diferentes dos outros tipos primitivos, como os maiores long e double, que mesmo sendo os maiores, ainda tem limites.

- BigDecimal, para números decimais;
- BigInteger, para números inteiros.
```
		BigDecimal _a = new BigDecimal("0.03");
		BigDecimal _b = new BigDecimal("0.04");
		BigDecimal _c = _b.subtract(_a);        // o resultado é correto, 0.01
		System.out.println(_c);    

        BigDecimal bd1 = new BigDecimal("1234567890.0987654321");
		BigDecimal bd2 = new BigDecimal("987654321.9876543210");
		System.out.println(bd1.add(bd2));         

        System.out.println(bd1.multiply(bd2));          // multiplicação
        System.out.println(bd1.divide(new BigDecimal(2)));   // divisão
```
Podemos criar um BigInteger, baseados em strings e em números, podendo fazer diversar operações com ele também.
```
		BigInteger bi = new BigInteger("10000000000000000000");
		System.out.println(bi);
```