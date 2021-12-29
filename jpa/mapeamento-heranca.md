Para fazermos mapeamento de Heranças podemos utilizar duas estrategias.
- SINGLE_TABLE: embora no java tenhamos as subclasses, podemos no banco de dados ter apenas uma tabela, um tabelão. Para isso, na classe mãe utilizamos a anotação @Inheritance, com o argumento strategy recebendo SINGLE TABLE, e classificar as classes filhas como entidade.
```
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
```
- JOINED: cria-se uma tabela para cada subclasse e coloca-se FKs para relacionar as tabelas.
@Inheritance(strategy = InheritanceType.JOINED)