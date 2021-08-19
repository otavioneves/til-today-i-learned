Os métodos são linhas de código que se repetiriam em vários pontos, e para otimizar o desenvolvimento e melhorar a manutenção do código, cria-se padrões com essas linhas, para que quando seja necessário utilizar essa parte, apenas se referencia o método e ele seja iniciado.<br>
O método é feito fora do método main, com a seguinte sintaxe:
```
static void imprimirTraco() {
		System.out.println("----------------------------------------------");
```
Dentro do código do método main, chama-se o método conforme abaixo:
```
imprimirTraco();
```
É possível que o método receba parâmetros, conforme abaixo:
```
    public static void main(String[] args) {

    	String[] cursos = new String[] {"Java EE", "Spring", "Java OO Avançado"};

	    System.out.println("Escolha dentre os cursos abaixo: ");

        iterarEExibirPosicoesDoVetorString(cursos);

    }


    static void iterarEExibirPosicoesDoVetorString(String[] vetor) {
		for(int i = 0; i < vetor.length; i++) {
			System.out.println("[" + i + "] " + vetor[i]);
		}
	}
```
É também possível que o método retorne valores para o código, alterando o void (retorno vazio) pelo tipo da varíavel que será retornado, conforme abaixo:
```
    static Boolean verificarPosicaoEscolhidaPeloUsuario(Integer posicao, String[] vetor) {
		
        Boolean valida = posicao >= 0 && posicao < vetor.length;
		
        return valida;
	}
```