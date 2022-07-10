### Gerenciador de Memória
O gerencadiador de memória faz uso do conceito de hierarquia de memória.
- O armazenamento em disco é a forma mais básica para se entregar dados para o processador.
- Posteriormente vem a memória principal, que recebe dados do disco e disponibiliza para o processador, facilitando a entrega dos dados, pos a memória principal é mais rápido.
- Os registradores é uma memória mais próxima do processador aonde são guardados dados que são utilizados com mais frequência.
- A memória cache é intermediária entre registradores e memória principal.
As principais características do armazenamento de dados em um sistema computacional levam em conta:
- O tempo de acesso ao disposivo;
- A velocidade com que a operação deverá ser realizada;
- O custo da unidade de armazenamento;
- A capacidade de armazenamento do dispositivo.

Levando em conta essas características, ao realizar um projeto de sistema operacional, devemos definir a quantidade de cada tipo de memória necessária, para garantir que o futuro sistema seja, simultaneamente, eficiente e viável do ponto de vista financeiro, garantindo velocidade, custo e capacidade de armazenamento.

Cabe ao gerenciador de memória comandar a hierarquia da memória de modo a:
- alocar memória aos processos quando for necessário;
- liberar a memória, quando um processo terminar;
- tratar do problema de swapping, isto é, quando a memória é insuficiente.

