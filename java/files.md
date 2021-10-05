A classe Files disponibiliza um método de escrever informações em arquivos de texto. A sintaxe do método de escrever em um arquivo .txt é:
```
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.Scanner;

public class EscritaArquivos {

	public static void main(String[] args) throws IOException {
		Scanner scanner = new Scanner(System.in);

		ArrayList<String> linhas = new ArrayList<String>();

		for (int i = 0; i < 5; i++) {
			System.out.print("Jogador " + i + ": ");
			String nome = scanner.nextLine();

			linhas.add(nome);
		}

		Path arquivo = Paths.get("/tmp/aula/arquivo.txt");
		Files.write(arquivo, linhas);

		scanner.close();
		System.out.println("Fim...");
	}
}
```
A diferença do ArrayList pra um Array normal é que não precisamos passar a quantidade de linhas do array.<br>
Para a leitura de arquivos, utilizamos a seguinte sintaxe:
```
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;

public class LeituraArquivos {

	public static void main(String[] args) throws IOException {
		Path arquivo = Paths.get("/tmp/aula/arquivo.txt");
		
		List<String> linhas = Files.readAllLines(arquivo);
		
		for(int i = 0; i < linhas.size(); i++) {
			String nome = linhas.get(i);
			
			System.out.println("Jogador " + i + ": " + nome);
		}
	}
}
```