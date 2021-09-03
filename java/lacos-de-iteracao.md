Os lações de iteração são o `for` e o `while`.
- for: a estrutura básica do for é formada inicialmente por uma expressão inicial, uma expressão de verificação de continuidade  e a última expressão de ação que irá acontecer à cada volta;
```
    for(int i = 0; i < 5; i++ ) //iniciando com o contador (i) em 0, repetir o laço enquanto o i for menor que 5, e à cada laço incrementar 1 em i.
```
Dentro do laço for podemos usar o comando `break`, dentro de um if, para pararmos o for devido à alguma condição.<br>
Também podemos usar o comando `continue`, dentro de um if, para não realizar o laço devido à alguma condição.<br>
O for também pode ser utilizado com partes ausentes, porém é pouco comum:
- Faltando na condição:
```
int i = 0
for (;i<10;){
	System.out.println(i);
	i++
}
```
- Faltando no corpo:
```
int soma = 0;
for (int i = 1; i<5;soma+=i++);
```

- while: a estrutura básica do while é formada por uma expressão condicional, e dentro do laço é feito o incremento.
```
        int i = 0;
		while (i < 10) {
			i++;
		}
```
<br>
O laço for é mais para quando você tem uma quantidade de iterações conhecidas, mesmo que for através de uma varíavel. Já o while é mais utilizada para ser utilizado devido à uma condição.<br>
Dentro do while também tem a vantagem de poder utilizar uma varíavel já presente no código.<br>
Os comandos break e continue também são muito utilizados nos laços de iteração:
- break : usado para parar uma laço:
```
//break
        int i = 0;
		while (i < 10) {
			if (i == 5) {
				System.out.println("Vai parar!");
				break;
			}
			System.out.println(i + ": Um texto qualquer.");
			i++;
		}
```
- continue : usado para continuar o laço:
		int i = 0;
		while (i < 10) {
			if (i == 5) {
				System.out.println("Vai continuar...");
				i++;
				continue;
			}
			
			System.out.println(i + ": Um texto qualquer.");
			i++;
		}
```
- do while: nessa estrutura a mudança é que fazemos o bloco, para depois verificar novamente a condição. No while, verifica-se a confição inicialmente, para depois executar o laço.
```
		do {
			System.out.println("Mensagem");
		} while (y++ < 1);
```

EXEMPLO COM VALIDAÇÃO DE INFORMAÇÕES DO CURSO DA LOIANE:
```
*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

package com.loiane.cursojava.aula17.labs;

import java.util.Scanner;

/**
 *
 * @author loiane
 */
public class Exer03 {
    
    public static void main(String[] args){
        
        Scanner scan = new Scanner(System.in);
        
        boolean infoValida = false;
        String nome, sexo, estadoCivil;
        int idade;
        double salario;
        
        do {
            
            System.out.println("Entre com o nome:");
            
            nome = scan.next();
            
            if (nome.length() >= 3){
                infoValida = true;
            } else {
                System.out.println("Nome precisa no mínimo 3 caracteres.");
            }
        } while (!infoValida);
        
        
        infoValida = false;
        do {
            
            System.out.println("Entre com a idade:");
            
            idade = scan.nextInt();
            
            if (idade >= 0 && idade <= 150){
                infoValida = true;
            } else {
                System.out.println("Idade precisa ser entre 0 e 150.");
            }
        } while (!infoValida);
        
        
        infoValida = false;
        do {
            
            System.out.println("Entre com o salário:");
            
            salario = scan.nextDouble();
            
            if (salario > 0){
                infoValida = true;
            } else {
                System.out.println("Salário precisa ser maior que 0.");
            }
        } while (!infoValida);
        
        
        infoValida = false;
        do {
            
            System.out.println("Entre com o sexo:");
            
            sexo = scan.next();
            
            if (sexo.equalsIgnoreCase("f") ||
                    sexo.equalsIgnoreCase("m")){
                infoValida = true;
            } else {
                System.out.println("Sexo precisa ser 'f' ou 'm'.");
            }
        } while (!infoValida);
        
        infoValida = false;
        do {
            
            System.out.println("Entre com o estado civil:");
            
            estadoCivil = scan.next();
            
            if (estadoCivil.equalsIgnoreCase("s") ||
                    estadoCivil.equalsIgnoreCase("c") ||
                    estadoCivil.equalsIgnoreCase("v") ||
                    estadoCivil.equalsIgnoreCase("d")){
                infoValida = true;
            } else {
                System.out.println("Estado civil precisa ser 's', 'c', 'v' ou 'd'.");
            }
        } while (!infoValida);
        
        System.out.println("As seguintes informações foram coletadas:");
        System.out.println("Nome: " + nome);
        System.out.println("Idade: " + idade);
        System.out.println("Salário: " + salario);
        System.out.println("Sexo: " + sexo);
        System.out.println("Estado Civil: " + estadoCivil);
        
    }
}
```
