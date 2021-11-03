Podemos fazer um tuning do MySQL utilizando o tuning do hardware. Para ter o melhor hardware no servidor é:
- Dar preferência ao Sistema Operacional de 64 Bits;
- Verificar a relação entre RAM e base de dados, geralmente é metade da quantidade de RAM disponível do hardware;
- Verificar o tipo de Leitura de Disco, o I/O (ssd, sas, sata);
- Utilizar controladora de disco RAID.
<br>

Podemos também fazer um tunning através da varíaveis de ambiente. O comando SHOW STATUS mostra a situação atual das varíaveis de ambiente. Existem dois tipos de varíaveis, as GLOBAL e SESSIONS. A configuração fica disponível no arquivo my.ini ou my.cnf.
- Para melhorar a performance podemos aumentar o tamanho disponibilizado para tabelas temporárias, entre tantas outras modificações nas diversas varíaveis que existem.
- Os mecanismos de arzamento permitem que hava uma separação entre a armazenagem e o código principal do banco de dados. Os mais usados são o MyISAM, InnoDB e MEMORY. O MyISAM é problemático para gravações e rápido para consultas. O InnoDB é o mecanismo de armazenamento transacional mais utilizado, ou seja, um banco de dados onde o volume de transações é alto, diferente dos bancos de dados gerenciais, onde fazemos carga dos dados e depois só consultamos. O memory é o mais rápido para acessar os dados. O tipo padrão do MySQL é InnoDB.