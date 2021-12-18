Um recurso adicional do Maven são os plugins, que são adicionadas pelo pom.xml dentro da tag `<plugins>`. O plugin adiciona algum recurso para o build da aplicação. Por exemplo, podemos adicionar o plugin do jetty, colocando um servidor no Maven.<br>
Outro importante é o plugin jacoco, que mostra quantos porcento da aplicação estão sendo testados.
Podemos também configurar o proxy para o Maven ter acesso à internet. Fazemos essa configuração ficam no arquivo da pasta .m2, no arquivo settings.xml, que podemos criar.
```
  	<proxies>
  		<proxy>
  			<id>meu-proxy</id>
  			<active>true</active>
  			<protocol>http</protocol>
  			<host>http://ip</host>
  			<port>1234</port>
  			<username>username</username>
  			<password>password</password>
  		</proxy>
  	</proxies>
```
