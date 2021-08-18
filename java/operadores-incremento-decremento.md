Os operadores de incremento e decremento são utilizados para incrementar ou decrementar um número. Utilizamos os argumentos `++` e `--`.
```
Integer numero = 10;
numero++;

Integer numero = 10;	
numero --
```

Como pode ser visto abaixo, utilizando o operador do lado direito de uma variável, primeiro à variável é incrementada e depois é atribuída à outra varíavel. Utilizando o operador do lado esquerdo da varíavel, primeiro se atribuí e depois incrementa.

```
Integer numero = 10;
Integer numero02 = ++numero; // Primeiro incrementa e depois passa o valor para a variável "numero02"
Integer numero02 = numero++; // Passa o valor para a variável "numero02" e depois incrementa.
System.out.println("Número: " + numero + ", " + "Número02: " + numero02);
```


