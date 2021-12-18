Podemos fazer o build através do comando `mvn compile` no terminal. Podemos antes rodar um `mvn clean` para limpar e atualizar os repositórios.<br>
Podemos adicionar um plugin para definirmos qual a versão do Java a ser utilizada.
```
  	<build>
		<plugins>
			<plugin>
				<artifactId>maven-compiller-plugin</artifactId>
				<configuration>
					<source>11</source>
					<target>11</target>
				</configuration>
			</plugin>
		</plugins>  	
  	</build>
```
Para rodarmos os testes automatizados podemos utilizar o comando `mvn test`.<br>
Para gerar o jar ou o war do projeto, o pacote, usamos o comando `mvn package`, que gera um jar ou um war de acordo com as configurações do projeto. Ele faz toda a compilação e roda os testes, e joga os arquivos no repositório target.<br>
O comando `mvn install` instala o pacote no nosso repositório local.<br>
O comando `mvn deploy`, faz o deploy, por exemplo, pode implantar o pacote em um repositório remoto.<br>
Podemos usar a tag <packaging> para forçar o arquivo de saída, jar ou war. Podemos rodar mais de um goal por vez
```
mvn clean compile teste package
```
Temos muitos outros recursos, porém esses são os principais. Pelo Eclipse podemos ir em Run As e rodar o goal que nós queremos.