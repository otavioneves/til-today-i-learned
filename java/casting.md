O casting é quando instanciamos um objeto de uma classe através de uma classe maior ou menor.
- Upcasting
```
        Aluno aluno = new Aluno();
		Pessoa pessoaAluno = aluno; //upcasting
		
		Pessoa aluno2 = (Pessoa) new Aluno(); //upcasting manual, convertendo o tipo Aluno em Pessoa.
```
- Downcasting
```
        Pessoa aluno3 = new Pessoa(); //downcasting
		Aluno aluno4 =  (Aluno) aluno3; // downcasting com conversão manual, convertendo um objeto de Pessoa em Aluno.
```