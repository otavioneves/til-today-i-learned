O processo é um programa que está sendo executado. As threads são a menor unidade de código que pode ser executada, podendo executar uma ou mais tarefas por momento.<br>
Para criar uma thread podemos extender a classe Thread ou implementar a interface Runnable.
- start: inicia o método run;
- run: executa a tarefa da thread;
- sleep: coloca a thread para dormir por alguns milisegundos.
### Extendendo a Classe Thread
```
public class Teste {
	public static void main(String[] args) {
		
		MinhaThread thread = new MinhaThread("Thread #1", 600);

	}
}
```
```
public class MinhaThread extends Thread {

	private String nome;
	private int tempo;

	public MinhaThread(String nome, int tempo){
		this.nome = nome;
		this.tempo = tempo;
		start();
	}

	public void run(){

		try {
			for (int i=0; i<6; i++){
				System.out.println(nome + " contador " + i);
				Thread.sleep(tempo);
			}
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		
		System.out.println(nome + " terminou a execução");
	}
}
```
### Implementando a interface Runnable - na hora de instanciar a thread no método main, utiliza o construtor com o Runnable, onde passamos a própria classe que implementa a interface Runnable como argumento.
```
public class Teste {
	public static void main(String[] args) {
		
		MinhaThreadRunnable thread1 = new MinhaThreadRunnable("#1", 900);
		//Thread t1 = new Thread(thread1);
		//t1.start();
	}
}
``` 
```
public class MinhaThreadRunnable implements Runnable {

	private String nome;
	private int tempo;

	public MinhaThreadRunnable(String nome, int tempo){
		this.nome = nome;
		this.tempo = tempo;
		Thread t = new Thread(this);
		t.start();
	}

	@Override
	public void run() {

		try {
			for (int i=0; i<6; i++){
				System.out.println(nome + " contador " + i);
				Thread.sleep(tempo);
			}
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		System.out.println(nome + " terminou a execução");
	}
}
```
- Quando extendemos a classe Thread, o único método que precisa ser sobreposto é o run.
- Quanto implementamos a classe Runnable, também precisamos implementar o método run.
- Com a Classe Runnable, podemos extender qualqur outra classe.
- Se não for sobrepor qualquer outro método da classe Thread, pode ser melhor usar a classe Runnable.
Para executar algo somente após uma thread ser finalizada, podemos usar o método `isAlive`, ou seja, para verificar se a thread está viva.<br>
Também podemos usar o método `join`, que espera a execução da thread para depois que a thread finalizar.
```
		MinhaThreadRunnable thread1 = new MinhaThreadRunnable("#1", 500);
		MinhaThreadRunnable thread2 = new MinhaThreadRunnable("#2", 700);
		MinhaThreadRunnable thread3 = new MinhaThreadRunnable("#3", 800);

		Thread t1 = new Thread(thread1);
		Thread t2 = new Thread(thread2);
		Thread t3 = new Thread(thread3);

		t1.start();
		t2.start();
		t3.start();

		try {
			t1.join();
			t2.join();
			t3.join();
		} catch (InterruptedException e) {
			e.printStackTrace();
		}

		System.out.println("Programa finalizado");
```
É possível definir a prioridade das threads, não com 100% de certeza, é o `setPriority()`, podendo definir a prioridade de 1 a 10, com 10 o mais prioritário, e a prioridade MÍNIMA, NORMAL E MÁXIMA.<br>
Quando duas ou mais threads precisar acessar o mesmo recurso, fazemos a sincronização das threads, para que cada uma acesse de cada vez, evitando conflito na execução. A palavra chave `synchronized` é utilizada ao definir o método, e ela deixa registrado que apenas uma thread pode acessar esse método por vez.<br>
No caso de um recurso que já está sendo utilizado por uma thread e uma outra thread tenta acessar esse recurso, ela irá ficar esperando e bloqueraá o objeto, impedindo que outra threads acessar o mesmo. Nesse caso a melhor solução para não causar problemas é liberar temporariamente o controle do objeto permitindo que outra thread seja executada, utilizando como um revezamento do uso do objeto entre as threads. Os seguintes métodos são utilizados para tal:
- `wait` = bloqueia a execução da thread temporariamente, ou seja, coloca a thread em modo de espera. A thread fica em modo de espera até que seja notificada;
- `notify` = notifica uma thread que estava esperando, ou seja, retorna a execução da thread;
- `notifyAll` = notifica todas as threads, e a que tem prioridade mais alta ganha acesso ao objeto.

Os métodos abaixo foram desativadas no Java, porém podemos criar métodos que sigam o mesmo intuito desses métodos, porém de maneira segura.

- `suspend` = suspende temporariamente a execução da Thread;
- `resume` = retorna a execução da Thread;
- `stop` = interrompe a execução.

O deadlock pode acontecer com processos e com threads. O deadlock é quando uma thread quer utilizar um recurso bloqueado por outra thread. Para evitar o deadlock utilizamos os métodos wait e notify, para revezar o uso dos objetos que serão compartilhados. 