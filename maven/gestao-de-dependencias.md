As dependências são bibliotecas que o projeto depende para funcionar. Muitas vezes além das bibliotecas precisamos gerir também as versões que precisamos no projeto. Fazemos essa configuração através do arquivo pom.xml.
```
  <dependencies>
  	<dependency>
  		<groupId> </groupId>        // groupIs da dependência
  		<artifactId> </artifactId>      // artifactId da dependência
  		<version> </version>        // versão da dependências
  		<scope> </scope>	    //escopo do projeto, configurações de provisionamento do build
  	</dependency>  
  </dependencies>
```
Exemplo:
```
  <dependencies>
  	<dependency>
  		<groupId>junit</groupId>  
  		<artifactId>junit</artifactId>
  		<version>4.12</version>
  		<scope>test</scope>	
  	</dependency>  
  </dependencies>
```
Após salvar essa alteração, o maven faz automaticamente o download. Para sabermos o groupId e o artifactId podemos pesquisar no repositório do Maven, o mvnrepository. Caso essa dependência já exista no repositório do computador, ele não faz o download.<br>
Podemos configurar para que o maven adicione dependências de outros repositórios.
```
	<repositories>
		<repository>
			<id>spring-repo</id>
			<url>https://repo.spring.io/release</url>
		</repository>
	</repositories>
```
A ordem é verificar no cache local (repositório chamado .m2, que é um diretório oculto que fica no usuário home), se não encontrar ele vai procurar nos repositórios que configuramos e depois no repositório central do Maven. O repositório adicionado pode ser também um repositório privado, um repositório local.