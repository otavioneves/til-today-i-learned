Para fazer o import de uma classe estática utilizamos o modificador de acesso `static`, desse modo, não precisamos usar o nome da classe na hora de chamá-la no código principal.

```
import static java.lang.Math.pow;
import static java.lang.Math.sqrt;

public class StaticImport {

	public static void main(String[] args) {
		
		double a = 2;
		double b = 3;
		double c = 4;

		System.out.println(Math.pow(a, b)); \\com o static import, não precisamos fazer assim, podendo fazer conforme abaixo:
	    System.out.println(pow(a, b));

		System.out.println(Math.sqrt(c)); \\com o static import, não precisamos fazer assim, podendo fazer conforme abaixo:
		System.out.println(sqrt(c));
		
	}
}
```