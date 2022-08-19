### Seção 2
- Linguagem de máquina: que é composta de sequências de zero e um. Essa linguagem permite ao computador a realização de suas tarefas, sendo definida pelo seu projeto de arquitetura.

- Linguagem de montagem: que faziam usos de programas montadores (assemblers) para converter o código-fonte escrito em linguagem de montagem para a linguagem de máquina, a qual seria reconhecida pelo computador.

- Linguagem de alto nível: que executam tarefas com menos instruções. Elas fazem uso de programas, chamados compiladores, para converter o código-fonte para linguagem de máquina.

Enquanto os compiladores convertem código-fonte escrito em uma linguagem de alto nível para a linguagem de máquina, os interpretadores executam o código-fonte, ou uma versão convertida para a linguagem de baixo nível, isto é, para a linguagem mais próxima da linguagem de máquina. Cabe ao interpretador converter as solicitações recebidas para linguagem de máquina. Apesar dessa vantagem, a necessidade de leitura, interpretação e execução por parte dos interpretadores torna a sua execução mais lenta do que a dos programas compilados, que já estão em linguagem de máquina.<br>
O compilador é utilizado quando se tem certeza da arquitetura do sistema e não precisará de portabilidade. O interpretador gera um código em uma linguagem de baixo nível (que não é ainda uma linguagem de máquina) que pode ser utilizadas em diversas arquiteturas.<br>
A execução de programas com interpretadores é mais lenta, pois os programadas compilados já estão em linguagem de máquina.<br>

### Seção 3
- Firmwares são instruções executáveis armazenadas em memória não volátil (que não se perde quando o computador é desligado), voltadas, em grande parte, para operações de leitura. A utilização do firmware permite que os fabricantes de dispositivos utilizem chips programáveis, de uso geral, em vez de utilizarem hardware de uso personalizado.

- Middleware permite que uma aplicação seja executada em um computador e se comunique com uma outra, executada em um outro computador, quando ambos fazem parte de um sistema distribuído (n máquinas diferentes, sistemas diferentes, mas todas executam a mesma tarefa com o mesmo resultado). O middleware permite a execução de aplicações em ambientes de computação heterogêneos (sistemas, arquiteturas, diferentes), desde que estes façam uso de um middleware comum entre eles. O middleware faz uso de uma Application Programming Interface (API) – Interface de Programação de Aplicações –, isto é, um conjunto de rotinas e padrões definidos por um software, o qual permite que um aplicativo utilize os seus serviços sem a necessidade de se aprofundar na forma com que ele foi desenvolvido.<br>
O middleware fornece os serviços por meio de sua API, fazendo uso dos recursos suportados pelo sistema operacional que o hospeda. Por exemplo, o usuário solicita ao middleware
a atualização de tabelas de um banco de dados, para executar essa tarefa, o middleware faz uso da capacidade do sistema operacional de ler e gravar os arquivos desse banco de dados.

### Seção 4
- O processador é um componente de hardware e podem estar em alguns formatos, por exemplo: CPU (processador), DSP (coprocessador gráfico, que auxiliar o processamento).
- Os sistemas operacionais, dispõem de diferentes modos de execução: o modo usuário, em que o usuário poderá executar apenas um subconjunto de instruções, impedindo-o de acessar as informações de outro usuário ou mesmo de causar dano ao sistema operacional; e o modo núcleo (estado supervisor), no qual o processador pode acessar instruções privilegiadas e recursos, em nome dos processos.
- Os processadores Complex Instruction Set Computing (CISC) – Computação com Conjunto de Instruções Complexas - possuíam um conjunto de instruções que podiam executar diversas operações, em virtude disso, os programadores de linguagem de montagem podiam escrever o código-fonte dos seus softwares com um menor número de linhas, já que muitas das instruções, que antes faziam parte do software, estavam incorporadas no processador.
- Os processadores Reduced Instruction Set Computing (RISC) – Computação com Conjunto de Instruções Reduzidas –, nos quais as atividades mais comuns do processador deveriam ser executadas de maneira mais eficiente. Os processadores RISC seguiram caminho inverso dos processadores CISC. Neles, a complexidade da programação foi transferida do hardware para o código-fonte compilado.
- A Unidade de Controle (UC) é responsável pela busca das instruções na memória principal (MP), pela sua decodificação e execução. Para realizar essas atividades, ela faz uso da Unidade de Busca de Instrução, responsável por carregar as instruções em memórias de alta velocidade, isto é, os registradores de instruções, os quais permitem ao processador executá-las rapidamente; e da Unidade de Decodificação de Instrução, que realiza a interpretação da instrução e a encaminha para a Unidade de Execução.
- Os registradores são responsáveis por armazenar os dados para uso imediato pelo processador. A velocidade e a proximidade dos registradores com a UC permitem que o processador não fique ocioso.
- Os registradores possuem dois tipos: de propósito geral, que são utilizados para guardar as variáveis dos programas e permitem à CPU acessá-las sem ter de buscá-las na memória principal; e os registradores de propósito específico.
- A parte principal da Unidade de Execução é a Unidade de Lógica e Aritmética (ULA), que se assemelha muito a uma calculadora convencional, executando operações lógicas e aritméticas, com números inteiros ou reais.
- Os registradores de propósito geral ou específicos são responsáveis por trazer tipos de dados diferentes para a ULA. Cabe à UC decidir quais os registradores encaminharão seus dados para a ULA e informar qual operação (soma, multiplicação, divisão, AND, OR etc.) será realizada.
- A interface de barramento é responsável pela interação do processador com a memória e os outros dispositivos do sistema.
- Por meio da interface de barramento, os dados da memória principal são copiados para a memória cache do processador, a qual atinge velocidades muito mais altas que a memória
principal. Essa cópia aumenta a eficiência do processador por meio do acesso rápido aos dados e às instruções.
- A memória cache é classificada em dois níveis: o cache Nível 1 – Level 1 (L1) –, que é o nível mais rápido e mais caro, localizado dentro do processador; e o cache Nível 2 – Level 2 (L2) –, que é maior e mais lento que o L1. Normalmente localizado na placa principal (motherboard – mainboard – placa-mãe), ele vem sendo deslocado para o processador, para melhorar o seu desempenho.
- O termo sistema de multiprocessamento engloba qualquer sistema que contenha mais de um processador. Podemos citar como exemplos de sistemas multiprocessados os notebooks, os quais possuem dois processadores, e os servidores de aplicação ou bancos de dados, hospedados em datacenters, 5 que possuem vários processadores.

### Seção 5
- Na maioria das tecnologias, podemos obter memórias menores, as quais são mais rápidas do que memórias maiores. As memórias mais rápidas estão, geralmente, disponíveis em números menores de bits.
- A hierarquia de memória é um esquema de categorização da memória, em que a mais rápida e mais cara fica no topo da hierarquia, enquanto a mais lenta e mais barata fica na base.
- A memória principal de um sistema computacional corresponde ao nível mais baixo de armazenamento de dados, dentro da hierarquia de memória, que o processador pode acessar diretamente.
- Os registradores internos, a memória cache e a memória principal são considerados meios de armazenamento voláteis, isto é, quando o fornecimento de energia do computador é interrompido, os dados armazenados são perdidos.
- A memória secundária, composta de dispositivos de armazenamento secundário e terciário, por exemplo: disco rígido (HD – Hard Disk), fita magnética, CD, DVD etc.
- O sistema operacional faz uso de um mecanismo chamado memória virtual (segmentação e/ou paginação) para iludir o usuário, fazendo-o acreditar que a memória total do seu computador é a soma da memória principal e da memória secundária. Esse mecanismo permite a transferência dos blocos de informação entre essas duas memórias, automaticamente, sem a intervenção e o conhecimento do usuário.
- O armazenamento terciário vem como uma solução para sistemas que necessitam de níveis de memória superiores ao que o armazenamento secundário oferece. Essa extensão é feita por meio do armazenamento de dados em fitas magnéticas, catalogadas e acessadas por braços robóticos, as quais armazenam dados importantes, porém com uma frequência de acesso inferior aos que estão sendo armazenados no disco rígido.
- A memória principal, muitas vezes chamada de RAM (Random Access Memory – Memória de Acesso Aleatório), é a locomotiva do sistema de memória. A memória principal é uma memória
volátil, isto é, ela perde o conteúdo quando o fornecimento de energia do sistema é interrompido.
- Um outro exemplo de memória volátil, utilizada pelos computadores, é a memória Complement-ary metal–oxide–semiconductor (CMOS) – Metal-óxido-semicondutor de simetria complementar –, utilizada para manter a data e a hora do computador atualizadas. A memória CMOS é alimentada por uma pequena bateria, a qual garante o funcionamento regular do relógio do computador, mesmo que ele esteja desligado.
- Alguns computadores fazem uso de memória aleatória não volátil. Podemos citar, como exemplo, a memória ROM (Read Only Memory – Memória Somente de Leitura), que já vem programada de fábrica e não pode ser utilizada pelo usuário. O processo de inicialização do computador, feito pelo carregador (bootstrap loader) é gravado nessa memória ROM, que é uma memória rápida e de baixo custo.
- Para resolver esse problema, o computador faz uso do armazenamento secundário (armazenamento 70 Sistemas Operacionais persistente ou auxiliar), no qual ele armazena grande quantidade de dados permanentes a um baixo custo, sendo estes mantidos mesmo que o computador seja desligado.


### Seção 6
- A forma mais comum de armazenamento secundário nos computadores é o disco rígido.
- O armazenamento no disco rígido é duas ordens de magnitude 6 mais barato, por bit, do que o da memória RAM. Porém, o tempo de acesso aos dados é cerca de três ordens de magnitude mais lento. O motivo dessa lentidão reside no fato de o disco rígido ser um dispositivo mecânico.

### Seção 7
- Um barramento é um conjunto de pistas, ou de outras conexões elétricas, que transportam informações entre dispositivos de hardware. Como tipos de barramentos, podemos citar:<br>
a. os barramentos de dados – são responsáveis pelo transporte de dados;<br>
b. os barramentos de endereços – armazenam e informam o endereço, em que os dados estão armazenados;<br>
c. as portas – permitem a conexão entre dois dispositivos;<br>
d. os canais de E/S – permitem a realização de operações de E/S por meio de um barramento compartilhado entre vários dispositivos. Os canais de E/S podem tentar acessar a memória ao mesmo tempo que o processador. Para evitar a colisão no barramento, um dispositivo de hardware, chamado controlador, fica responsável por esse processo.
- O Barramento Frontal (FSB – Front Side Bus) é o responsável por conectar o processador à memória principal. O desempenho do computador aumenta à medida que há um aumento na taxa de dados transferida pelo barramento frontal.
- O Barramento de Interconexão de Componente Periférico (PCI – Peripheral Component Interconnect) é o responsável pela conexão dos dispositivos periféricos – como placas de vídeo, de som ou de rede – ao resto do computador.
- Utilizada na renderização de objetos 3D em tempo real, a Porta Gráfica Acelerada (AGP – Accelerated Graphics Port) é responsável por conectar placas gráficas que utilizam grandes quantidades de memória RAM para realizarem suas atividades.
- O barramento Universal Serial Bus (USB) – Barramento Serial Universal
– Foi criado para realizar a conexão dos dispositivos de E/S, considerados lentos, como mouses e teclados, ao computador. Uma grande vantagem na sua utilização é que os dispositivos USB fazem uso do mesmo driver, portanto não é necessário instalar um novo driver cada vez que um novo dispositivo USB é acoplado ao computador, nem mesmo reiniciar a máquina.
- O barramento Small Computer System Interface (SCSI) – Interface de Pequeno Sistema de Computadores – foi criado para a conexão de dispositivos de alto desempenho e alto consumo de banda, como os discos rígidos rápidos, os scanners etc.
- Um dispositivo de E/S é constituído por duas partes, um controlador, isto é, um chip ou um conjunto de chips responsável pelo gerenciamento do dispositivo, e o dispositivo propriamente dito. O sistema operacional se comunica com o controlador, solicitando a ele que os dados sejam lidos pelo dispositivo, quando é realizada uma operação de entrada, ou enviados para o dispositivo, quando é realizada uma operação de saída.
- 