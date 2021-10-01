No Java, sempre que instanciamos um objeto nós alocamos memória pra esse objeto e terá uma referência. Essa referência fica na pilha do programa ou na pilha do método, que aponta para o endereço de memória Heap. O tamanho do objeto depende dos seus atributos, métodos, etc.<br>
Quando um método é finalizado ou os objetos não são mais referenciados no programa, a memória no Heap continua "reservada" para esse objeto, gerando um "lixo", ocupando memória desnecessária. O garbagge colector passa para apagar esses lixos, ele marca as referências que não estão sendo mais utilizadas pelo programa, e depois apaga. Depois de apagar, ele otimiza a memória, reorganizando a ordem das memórias alocadas.
- Para obtermos a memória que está sendo utilizada pelo programa podemos usar o runtime, uma classe do java.lang utilizada para capturar a memória em tempo de execução. O padrão utilizado é o singleton, ou seja, uma instância da classe(Runtime) por projeto
```
	public static void obterMemoriaUsada(){
		
		final int MB = 1024 * 1024;
		
		Runtime runtime = Runtime.getRuntime(); //singleton
		
		System.out.println((runtime.totalMemory() - runtime.freeMemory())/MB);
		
	}
```
- Para forçar o garbagge colector ser executado, utilizamos a seguinte maneira. (Dificilmente é utilizado no dia a dia)
```
		Runtime.getRuntime().runFinalization();
		
		Runtime.getRuntime().gc();
```
- Para ver de maneira visual utilizamos os profilings utilizamos o terminal: