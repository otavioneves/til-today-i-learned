Os vetores, ou arrays, são as estruturas de dados mais simples que existe. Um array armazena uma sequência de valores onde todos são do mesmo tipo.
No exemplo, a classe Vetor é iniciada da seguinte maneira.
```
private String[] elementos;         // criando o array
private int tamanho;        // atributo que irá controlar o tamanho do vetor

public Vetor(int capacidade){       // construtor passando a capacidade de elementos do vetor que será criado
	this.elementos = new String[capacidade];        // cria um vetor com a capacidade passada
	this.tamanho = 0;
}
```
- Para adicionar um item no vetor podemos fazer da seguinte maneira:
### OPÇÃO 1: pouco performático, pois roda o vetor inteiro se necessário
```
public void adiciona(String elemento){        // método para adicionar um elemento no vetor, passando o elemento à ser adicionado
	for (int i=0; i<this.elementos.length; i++){        // iteração do vetor
		if (this.elementos[i] == null){         // se for null, quer dizer que está vazio
			this.elementos[i] = elemento;       // estando vazio, adiciona o elemento passado na posição
			break;      // para o método
		}
	}
}
```
### OPÇÃO 2: cria um atributo int tamanho, na classe, que controla o tamanho real do vetor. Tem a limitação da questão do tamanho e do tamanho do vetor criado.
```
public void adiciona(String elemento) throws Exception{
	if (this.tamanho < this.elementos.length){      // verifica se a varíavel tamanho é menor que a quantidade de elementos do vetor, se sim, ele irá adicionar a string passada no elemento definido pelo número da variavel tamanho, que inicia em zero
		this.elementos[this.tamanho] = elemento;        // a variavel tamanho inicia em zero, é incrementa um a cada adição, ou seja, vai adicionando os elementos no zero, no um, no dois, etc...
		this.tamanho++;
	} else {
		throw new Exception("Vetor já está cheio, não é possível adicionar mais elementos");    
	}
}
```
### OPÇÃO 3: no lugar de lançar uma exception, retorna um boolean
```
public boolean adiciona(String elemento) {      // irá retornar boolean, retorna true caso seja possível adicionar e false caso não adicione, entrando no lugar da Exception, que pode ser tratado depois
	this.aumentaCapacidade();
	if (this.tamanho < this.elementos.length){
		this.elementos[this.tamanho] = elemento;
		this.tamanho++;
		return true;
	} 
	return false;
}
```
O método tamanho apenas retorna o tamanho real do vetor:
```
public int tamanho(){
	return this.tamanho;
}
```
O método para imprimir todos os elementos do vetor, podemos usar a Classe Arrays somada ao método toString, recebendo de parâmetro o nosso vetor. No código abaixo, imprimir apenas os elementos dos vetores que tem algo, as vazias não aparece.
```
@Override
public String toString() {
		
	StringBuilder s = new StringBuilder();      // utilizamos a Classe StringBuilder para concatenar string
	s.append("[");      // o método .append da Classe StringBuilder adiciona uma string, no caso estamos adicionando o abrir dos colchetes.
	
	for (int i=0; i<this.tamanho-1; i++){
		s.append(this.elementos[i]);        // adicionado o elemento
		s.append(", ");     // adicionando a virgula
	}
	
	if (this.tamanho>0){
		s.append(this.elementos[this.tamanho-1]);               // adicionado o elemento
	}
	
	s.append("]");      // já aqui, com o método .append da Classe StringBuilder, estamos adicionado uma string, no caso estamos adicionando o fechar dos colchetes.
	
	return s.toString();
}
```
- Para buscarmos um elemento podemos fazer da seguinte maneira, buscando um elemento de determinada posição.
### OPÇÃO 1: maneira mais simples de fazer, passando a posição, retorna o elemento da posição buscada. Não é a melhor maneira, pois pode ser digitada uma posição que seja nula ou que não existe, precisa de uma implementação de if.
```
public String busca(int posicao){           // busca o elemento de uma determina posição passada
	if (!(posicao >= 0 && posicao < tamanho)){          // quando a posição não puder ser acessada, por n motivos, lança uma exception, nesse caso a IllegalArgumentException.
		throw new IllegalArgumentException("Posição inválida");
	} 
	return this.elementos[posicao];         // quando a posição for válida, retorna o elemento da posição buscada.
}
```
### OPÇÃO 2: nesse modo, passando o elemento à ser buscado, o método retorno um int, que é a posição que foi encontrado o string passado. Ou seja, verifica se o elemento existe no vetor, fazendo uma busca sequencial
```
public int busca(String elemento){          // busca o elemento buscando entre as posições do vetor
	for (int i=0; i<this.tamanho; i++){         // itera o vetor
		if (this.elementos[i].equals(elemento)){        // compara o elemento da posição i que está sendo iterada com a String passada.
			return i;           // retorna a posição, informando a posição de aonde está essa string.
		}
	}
	return -1;      // retorna -1 caso o elemento passado não exista no vetor.
}
```
- Para adicionar um elemento em qualquer posição ser perder os elementos originais e ficando com um elemento a mais no vetor
```
public void adiciona(int posicao, String elemento){          // adiciona o elemento na posição passada
	
	if (!(posicao >= 0 && posicao < tamanho)){          // verifica se a posição passada é valida ou não
		throw new IllegalArgumentException("Posição inválida");         // caso seja posição inválida, lançamos uma exception
	}
	
	this.aumentaCapacidade();       // método que aumenta a capacidade do vetor caso o tamanho seja igual o tamanho do vetor
			
	for (int i=this.tamanho-1; i>=posicao; i--){            // for para iterar o vetor, porém iniciando no final do vetor e voltando de posição em posição. indo até a posição que passamos.
		this.elementos[i+1] = this.elementos[i];            //  passando o elemento para uma posição à frente
	}
	this.elementos[posicao] = elemento;         // quando chegar na posição e todos os elementos até ali tiverem sido passados para frente, colocamos o elemento na posição desejada
	this.tamanho++;             // e aumenta o tamanho do vetor.
}
```
- Para aumentarmos a capacidade do vetor, temos que passar todos os dados de um vetor para um novo vetor com capacidade maior:
```
private void aumentaCapacidade(){
	if (this.tamanho == this.elementos.length){         // caso o caso o tamanho seja igual ao tamanho do array
		String[] elementosNovos = new String[this.elementos.length * 2];        // cria um novo vetor com o dobro de tamanho
		for (int i=0; i<this.elementos.length; i++){            // for para iterar o vetor
			elementosNovos[i] = this.elementos[i];          // adiciona os elementos antigos nos novos
		}
		this.elementos = elementosNovos;            // faz o vetor elementos receber o novo vetor
	}
}
```
- Para remover um elemento em qualquer posição ser perder os elementos originais e ficando com um elemento a menos no vetor
```
public void remove(int posicao){
	if (!(posicao >= 0 && posicao < tamanho)){          // verifica se a posição passada é valida ou não 
		throw new IllegalArgumentException("Posição inválida");         // caso seja posição inválida, lançamos uma exception
	}
	for (int i=posicao; i<this.tamanho-1; i++){         // for para iterar o vetor, porém iniciando na posição passada,e indo para frente de posição em posição até o fim do vetor
		this.elementos[i] = this.elementos[i+1];        // traz os elementos uma posição para tras
	}
	this.tamanho--;         // diminui um do tamanho
}
```
Para removermos um elemento sem saber sua posição, podemos usar o método busca, que retorna a posição do vetor, e passar essa posição encontrada pro método passado.
- Para generelizar o tipo do vetor para que o vetor possa funcionar com qualquer tipo de dados ou classes no java podemos passar a Classe Object na construção do vetor, podendo assim receber toda classe e tipo, sendo possível até ter mais de um tipo por vetor, porém isso vai contra o conceito de vetor.
```
private Object[] elementos; 
```
- Para configuar o tipo de vetor dinamicamente, utilizamos o Generics, podendo assim na declaração passar o tipo que queremos usar dentros dos <>:
```
public class Lista<T> {         // criamos uma classe com o T entre os <>, declarando que o que o vetor receberá é o Type, ou seja, tipos, podendo colocar String, int, double, etc.

	private T[] elementos;          // coloca o tipo T, de tipo, na hora de criar

}
```
Para fazer o construtor, utilizamos o casting do tipo Object pro tipo T:
```
public Lista(int capacidade){
	this.elementos = (T[]) new Object[capacidade]; //solução do livro effective Java
	this.tamanho = 0;
}
```
Para instanciar:
```
Lista<Contato> vetor = new Lista<Contato>(1);

	// ou

Lista<String> vetor = new Lista<String>(1);

    // ou qualquer outro tipo
```
Para utilizar em qualquer método, utilizamos o T como tipo:
```
public int busca(T elemento){               // utiliza o tipo T
	for (int i=0; i<this.tamanho; i++){
		if (this.elementos[i].equals(elemento)){
			return i;
		}
	}
	return -1;
}
```
Depois de passar o tipo na hora de instanciar, seja String, double, int ou qualquer Classe, ele só receberá esse tipo de elemento. 