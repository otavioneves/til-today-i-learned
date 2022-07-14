A recursividade dentro de métodos é quando um método chama ele mesmo, a partir de uma condição.
```
    static void iterarEExibirPosicoesDoVetorString(String[] vetor) {
		iterarEExibirPosicoesDoVetorString(vetor, 0);
	}
	
	static void iterarEExibirPosicoesDoVetorString(String[] vetor, Integer i) {
		imprimir("[" + i + "] " + vetor[i]);
		
		if (++i < vetor.length) {
			iterarEExibirPosicoesDoVetorString(vetor, i);
		}
	}
```

Na recursividade, uma função chama a si mesma repetidamente, até atingir uma condição de parada. No caso de Java, um método chama a si mesmo, passando para si objetivos primitivos. Cada chamada gera uma nova entrada na pilha de execução, e alguns dados podem ser disponibilizados em um escopo global ou local, através de parâmetros em um escopo global ou local.
```
public class FuncaLambda {
    public static void main(String[] args) {
        System.out.println(fatorial(5));
    }

	public static int fatorial (int value) {
		if (value == 1){
			return value;
		} else {
			return value * fatorial((value-1));
		}
	}	
}
```
A recursividade trabalha com a pilha de execução.<br>
Para otimizar uma recursividade podemos criar um map para fazer como cachê salvando resultados anteriores que podem ser reutilizados em outras chamadas do mesmo método.