Os Resources Bundle são arquivo que ajudam a obter configurações de acordo com o locale da aplicação e para localizar ou internacionalizar os projetos. O Resource Boundle fica na src do projeto. O tipo dele é .properties, como por exemplo: meu-texto.properties.
```
		System.out.println("Locale atual " + Locale.getDefault());          // o método getDefault pega o locale padrão do sistema
		ResourceBundle rb = ResourceBundle.getBundle("meu-texto");          // chama o arquivo criado, no caso, meu-texto.
		
		System.out.println("Hello EN: " + rb.getString("hello"));           // pega a string nas chaves do arquivo rb e retorna a tradução que está escrito no arquivo que foi feito
		System.out.println("World EN: " + rb.getString("world"));           // pega a string nas chaves do arquivo rb e retorna a tradução que está escrito no arquivo que foi feito

```
Podemos também passar o arquivo e o locale.
```
		rb = ResourceBundle.getBundle("meu-texto", new Locale("pt_BR", "pt_BR"));   // puxando o arquivo meu-texto que contém pt_BR no nome
		
		System.out.println("Olá pt_BR: " + rb.getString("hello"));          // pega a string nas chaves do arquivo rb e retorna a tradução que está escrito no arquivo que foi feito
		System.out.println("Mundo pt_BR: " + rb.getString("world"));        // pega a string nas chaves do arquivo rb e retorna a tradução que está escrito no arquivo que foi feito
```