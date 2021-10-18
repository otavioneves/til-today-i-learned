Os testes automatizados são como uma classe que testará o funcionamento de uma outra classe, executando todas as suas possibilidades de funcionamento.<br>
Para executar testes automatizados de maneira mais produtiva em Java, podemos utilizar o JUnit, que é uma biblioteca padrão para escrita de testes automatizados em Java. O foco do JUnit é em testes de unidades, ou teste unitários.<br>
Para fazermos o teste, criamos uma classe que tem o mesmo nome da classe testada somada a palavra Teste, por exemplo, CalculadoraTest, para testar a classe Calculadora. Nessa classe teremos um método por cenário de teste.<br>
Podemos adicionar o Junit de várias maneira, umas delas é utilizar a anotação `@Test` no método, com isso podemos rotar o teste. Para verificar se o teste passou podemos utilizar a classe `Assert`, para fazer assertivas, ou verificações. Essa classe possui vários método estáticos, como o `assetEquals`, que recebe o valor esperado e a varíavel que será verificada se está com esse valor.
```
import org.junit.Assert;
import org.junit.jupiter.api.Test;

public class CalculadoraTest {
	
	@Test
	public void deveriaSomarDoisNumerosPositivos() {
		Calculadora calc = new Calculadora();
		int soma = calc.somar(3, 7);	
		
		Assert.assertEquals(10, soma);
	}
	
}
```
Após rodar o JUnit Test e caso tudo fique verde é que todos os testes passaram, se algum falhou, podemos rastrear qual teste falhou.<br>
Outra maneira de adicionar o JUnit é adicionar ele via dependências no pom.xml
```
	<dependencies>
		<dependency>
			<groupId>org.junit.jupiter</groupId>
			<artifactId>junit-jupiter-engine</artifactId>
			<version>5.7.0</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
```
Podemos criar um caso de teste ao invés de uma clase, diretamente na IDE, como o Eclipse, selecionando Other e filtrando e buscando JUnit Teste Case.
- Funcionalidade.
```
import java.math.BigDecimal;
import java.math.RoundingMode;
import br.com.alura.tdd.modelo.Funcionario;

public class BonusService {

	public BigDecimal calcularBonus(Funcionario funcionario) {
		BigDecimal valor = funcionario.getSalario().multiply(new BigDecimal("0.1"));
		if (valor.compareTo(new BigDecimal("1000")) > 0) {
			valor = BigDecimal.ZERO;
		}
		return valor.setScale(2, RoundingMode.HALF_UP);
	}

}
```
- Teste
```
import static org.junit.jupiter.api.Assertions.assertEquals;
import java.math.BigDecimal;
import java.time.LocalDate;
import org.junit.jupiter.api.Test;
import br.com.alura.tdd.modelo.Funcionario;

class BonusServiceTest {

	@Test
	void bonusDeveriaSerZeroParaFuncionarioComSalarioMuitoAlto() {

		BonusService service = new BonusService();
		
		BigDecimal bonus = service.calcularBonus(new Funcionario("Otavio",LocalDate.now(),new BigDecimal("25000")));
		
		assertEquals(new BigDecimal("0.00"), bonus);
		
	}
	
	@Test
	void bonusDeveriaSerDezPorCentoDoSalario() {

		BonusService service = new BonusService();
		
		BigDecimal bonus = service.calcularBonus(new Funcionario("Otavio",LocalDate.now(),new BigDecimal("2500")));
		
		assertEquals(new BigDecimal("250.00"), bonus);
		
	}
	
	@Test
	void bonusDeveriaSerDezPorCentoParaSalarioDeExatamenteDezMil() {

		BonusService service = new BonusService();
		
		BigDecimal bonus = service.calcularBonus(new Funcionario("Otavio",LocalDate.now(),new BigDecimal("10000")));
		
		assertEquals(new BigDecimal("1000.00"), bonus);
		
	}	

}
```

Para testar um caso que o método lança uma Exception, podemos utilizar o método `assertThrows`, que recebe a exception que será lançada e um lambda da função verificada.

```
	@Test
	void semBonusParaFuncionarioComSalarioMuitoAlto() {

		BonusService service = new BonusService();
		assertThrows(IllegalArgumentException.class, () -> service.calcularBonus(new Funcionario("Otavio",LocalDate.now(),new BigDecimal("25000"))));

	}
```

Podemos também utilizar o try catch.

```
	@Test
	void semBonusParaFuncionarioComSalarioMuitoAltoUsandoTryCatch() {
		
		BonusService service = new BonusService();

		try {
			service.calcularBonus(new Funcionario("Otavio",LocalDate.now(),new BigDecimal("25000")));
// se passar da linha, que é a linha onde da uma Exception, podemos considerar o teste como falhou.
			fail("Não deu a excepetion!");
		} catch (Exception e) {
// aqui no catch podemos ver a mensagem que está sendo retornada dessa Excepetion está certa
			assertEquals("Funcionário com salário acima de R$10.000,00 não existe bônus.", e.getMessage());
		}

	}
```

As abordagens dos testes geralmente podem ser três:
- TESTAR UM VALOR QUE É DEVOLVIDO POR UM MÉTODO: Tem teste que chamamos um método, definimos um cenário para esse método, o método devolve o valor, e então fazemos um assert para verificar se o resultado devolvido é o esperado.
- TESTAR UM OBJETO QUE É MODIFICADO POR UM MÉTODO: Tem teste que chamamos um método porém ele é void, não devolve nada, mas modifica algum atributo desse objeto, e nesse caso fazemos o assert em cima do objeto que estamos passando para o método, como por exemplo, verificar o valor de algum dos seus atributos que foi modificado após chamarmos o método anterior.
- TESTAR UMA EXCEPTION: Tem teste que chamamos para verificar se certa exceção acontece em certa condição que deveria acontecer mesmo.
<br>
Da mesma maneira que refatoramos o código, também é uma boa prática refatorar os códigos do teste, a fim de deixar ele sempre atualizado e sempre manutenível.<br>
Por exemplo, podemos ver linhas em comum entre os testes e colocá-los para a classe de teste toda.<br>
Podemos também utilizar a anotação @Before Each do JUnit, que define que um método que definirmos será todado antes de inicializar cada teste.

```

	@BeforeEach
	public void inicializar() {
		service = new ReajusteService();
		funcionario = new Funcionario("Nome", LocalDate.now(), new BigDecimal("1000.00"));
	}
	
	
	@Test
	void reajusteDeveriaSerDeTresPorCentoQuandoODesempenhoForADesejar() {
		service.concederReajuste(funcionario, Desempenho.A_DESEJAR);
		assertEquals(new BigDecimal("1030.00"), funcionario.getSalario());
	}

```

Outras anotações são:
- AfterEach: assim como o BeforeEach, é utilizado para definirmos um método para ser rodado sempre após cada um teste de ser finalizados.
- BeforeAll: essa anotação define que um método, que tem que ser static, será rodado antes de todos o código de teste, porém será rodado apenas uma vez.
- AfterAll: essa anotação define que um método, que tem que ser static, será rodado depois de todos o código de teste, porém será rodado apenas uma vez.
<br>
Em caso de um método privado, nós não testamos, pois ele é um método utilitário que é utilizado apenas dentro da classe. O funcionamento dele acabará sendo testado quando chamarmos um método que utilizado esse método privado, testando assim o seu funcionamento.
<br>
Em uma aplicação não vamos testar todas as classes e todos os métodos, pois nem tudo tem complexidade ou necessidade de testar, devemos testar as classes que tem uma regra de negócio, que tem validações, cálculos, e também classes que tendem a sofrer alguma alteração no futuro.