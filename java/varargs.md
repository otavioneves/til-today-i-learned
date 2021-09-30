Para colocar mais de um parâmetro em um método, não sendo necessário definir anteriormente a quantidade de parâmetros, podemos utilizar o varargs. O varargs funciona dentro do espaço dos parâmetros de um método, onde utilizamos o tipo como Wrapper, pois o varargs aceita apenas Classes e os Wrappers são as classes de um tipo primitivo, instanciando um vetor. Com isso, todo o parâmetro digitado cai como um vetor, que será interado por um for dentro desse método.
```
public static void main(String[] args) {

		System.out.println(soma(1, 2, 3, 4, 5, 6, 7, 8, 9, 10));
	}

	static int soma(Integer... vetor){

		int total = 0;

		for (int i=0; i<vetor.length; i++){
			total += vetor[i];
		}

		return total;
	}
```

Caso seja necessário declarar outros parâmetros de outros tipos para esse método, devem ser declarados antes do varargs.

```

    static int soma(int a, int b, Integer... vetor){

		int total = 0;

		for (int i=0; i<vetor.length; i++){
			total += vetor[i];
		}

		return total;
	}
    
```