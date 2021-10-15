A serialização é transformar um objeto em um fluxo de bytes e bytes, ou fazer também o contrário. Para isso, utilizamos duas classes, a `ObjectOutputStream` e o `ObjectInputStream`, ambos são da biblioteca java.io.<br>
A serialização é muita utilizada para ligações entre JVMs, ou seja, na rede, enviando os dados em forma de bytes.<br>
- Transformando um string em um fluxo de bytes e persistindo em um arquivo binário .bin.
```
String nome = "Otavio Neves";

ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("objeto.bin"));		//criamos um ObjectOutputStream através de um FileOutputStream criado, que recebe o arquivo aonde esses bytes serão armazenados.

oos.writeObject(nome);		// o método writObject recebe um objeto e transforma em um fluxo de bytes
	
oos.close();
```
- Lendo esse arquivo que foi criado, que é um fluxo de bytes e transformando em uma string novamente.
```
ObjectInputStream ois = new ObjectInputStream(new FileInputStream("objeto.bin"));
		
String nome = (String) ois.readObject();		// o método readObject lê e devolve um Object, por isso precisamos fazer um parse para String
		
System.out.println(nome);
		
ois.close();
```
Para serializar qualquer objeto, como por exemplo uma classe de algum projeto, podemos fazer da seguinte maneira. Geralmente as classes não implementam a interface Serializable, que é uma interface que transforma a classe em serializável. Para que consigamos serializar uma classe criada por nós, precisamos implementar a interface Serializable na nossa classe.<br>
Para que funcione, no momento de serializar e desserializar utiliza o serialVersionUID, e esse ID precisam ser iguais. Para termos um serialVersionUID precisamos colocar um atributo static final na classe e colocarmos o ID necessário. Quando ocorre uma mudança na classe e não deixarmos travado o ID, o java irá gerar outro número para o ID. Por isso, precisamos definir esse ID e deixar forçado, porém isso não é 100% porque se mudarmos algum atributo, na hora de desserializar dará exception. Para cada mudança, principalmente em atributos, temos que aumentar 1 no ID, deixando ele sempre atualizado.
