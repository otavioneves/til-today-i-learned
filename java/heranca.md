As classes podem se relacionar utilizando também as heranças. As heranças são herdadas de uma classe mãe para uma classe filha, ou de uma superclasse para um subclasse.<br>
O conceito de herança é essencial para utilizarmos atributos e métodos que se repetem em classes diferentes, criando uma árvore com uma raiz e suas folhas.
- Raiz: classe inicial;
- Folha: classe final, que não pode herdar mais nenhuma classe.
Alguns conceitos importantes são sobre as classes e métodos abstratos e finais:
- Uma classe abstrata não pode ser instanciada. Só pode servir como progenitora.
- Um método abstrato pode ser declarado, mas não implementado na progenitora.
- Uma classe final não pode ser herdada de outra classe. É obrigatoriamente uma folha.
- Um método final não pode ser sobrescrito pelas suas subclasses, é obrigatoriamente herdado.
```
package aula11b;

public class Aula11 {

	public static void main(String[] args) {

		Visitante v1 = new Visitante();
		v1.setNome("Juvenal");
		v1.setIdade(22);
		v1.setSexo("Masculino");
		System.out.println(v1.toString());
		
		
		Aluno a1 = new Aluno();
		a1.setNome("Cláudio");
		a1.setMatricula(1111);
		a1.setCurso("Informática");
		a1.setIdade(16);
		a1.setSexo("Masculino");
		a1.pagarMensalidade();
		System.out.println(a1.toString());
		
		Bolsista b1 = new Bolsista();
		b1.setNome("Jubileu");
		b1.setMatricula(2222);
		b1.setCurso("Engenharia");
		b1.setIdade(20);
		b1.setSexo("Masculino");
		b1.setBolsa(12.5);
		b1.pagarMensalidade();
		System.out.println(b1.toString());
		
	}

}
```
```
package aula11b;

public abstract class  Pessoa {

	private String nome,sexo;
	private Integer idade;
	
	public void fazerAniver() {
		this.setIdade(this.getIdade() + 1);
	}
	
	@Override
	public String toString() {
		return "\nPessoa\nNome=" + nome + "\nSexo=" + sexo + "\nIdade=" + idade+"\n";
	}


	public String getNome() {
		return nome;
	}
	public void setNome(String nome) {
		this.nome = nome;
	}
	public String getSexo() {
		return sexo;
	}
	public void setSexo(String sexo) {
		this.sexo = sexo;
	}
	public Integer getIdade() {
		return idade;
	}
	public void setIdade(Integer idade) {
		this.idade = idade;
	}
	
}
```
```
package aula11b;

public class Aluno extends Pessoa {
	
	private Integer matricula;
	private String curso;
	
	public void pagarMensalidade() {
		System.out.println("Mensalidade paga do aluno " + this.getNome());
	}
	
	
	public Integer getMatricula() {
		return matricula;
	}
	public void setMatricula(Integer matricula) {
		this.matricula = matricula;
	}
	public String getCurso() {
		return curso;
	}
	public void setCurso(String string) {
		this.curso = string;
	}
	
}
```
```
package aula11b;

public class Bolsista extends Aluno {

	private Double Bolsa;
	
	public void renovarBolsa() {
		System.out.println("Bolsa renovada!");
	}
	
	@Override
	public void pagarMensalidade() {
		System.out.println(this.getNome() + " é bolsita. Pagamento facilitado.");
	}

	public Double getBolsa() {
		return Bolsa;
	}

	public void setBolsa(Double bolsa) {
		Bolsa = bolsa;
	}
	
	
}
```
```
package aula11b;

public class Visitante extends Pessoa {
	
}
```