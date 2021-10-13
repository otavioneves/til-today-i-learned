O Javadoc é utilizado para documentação do projeto. Podemos fazer uma espécio de comentário durante o código, informando o autor, versão, fazendo comentários das classes, dos parâmetros, métodos, exceptions, etc.<br>
Para inserir um comentário para o javadoc utilizamos a marção iniciando com /** e fechando com */.
```
/**
*
*@author Otavio Neves
*@version 0.1
*/
```
Para gerarmos o javadoc, após fazermos todas as marcações e comentários, vamos em Project e Generate Javadoc.<br>
Salvaremos o documento na pasta padrão do projeto. Após o OK, será criada uma página HTML que contém todas as informações do projeto. Foi criada uma pasta doc, e vários arquivos a partir dessa varredura de classes, mas o que nos interessa neste momento é o index, aonde está presente a documentação.<br>
Nessa documentação, todos os membros "public" são contemplados.<br>
Existem várias tags que podemos utilizar, elas são:
- @author (usado na classe ou interface)
- @version (usado na classe ou interface)
- @param (usado no método e construtor)
- @return (usado apenas no método)
- @exception ou @throws (no método ou construtor)
- @see
- @since
- @serial
- @deprecated