Sistema de Entrada e Saída
==========================

As duas principais tarefas de um computador são operações de E/S e
processamento, sendo que em alguns casos o processamento é até secundário. O
papel do sistema de E/S é controlar e gerenciar os dispositivos de E/S do
computador.

Como os dispositivos são muito diferentes entre si (considere um mouse, um drive
de disquete e uma impressora, por exemplo) são necessários vários métodos
diferentes para acessá-los, o que compõe o subsistema de entrada e saída. Além
disso, dispositivos de diferentes modelos e/ou fabricantes podem possuir certas
particularidades e precisam ser tratados de uma forma muito específica. Para
encapsular estes detalhes existem os módulos de driver de dispositivo (*device
driver modules* ou simplesmente "driver"). Os drivers de dispositivo tratam das
peculiaridades de cada dispositivo, mas apresentam uma interface padrão para o
subsistema de entrada e saída.

Características do dispositivo
------------------------------

- Modo de transferência: Caractere/Bloco
- Método de acesso: Sequencial/Aleatório
- Sincronização de transferência: Síncrono/Assíncrono
- Compartilhamento: Dedicado/Compartilhável
- Velocidade do dispositivo: Latência, tempo de busca, taxa de transferência,
retardo entre operações
- Direção de E/S: Somente leitura, somente escrita, leitura/escrita

Driver de dispositivo
=====================

O driver é a parte do SO que trabalha mais próxima do dispositivo e sua
controladora. Apenas o driver precisa saber os detalhes da operação do
dispositivo. Um driver em geral trata de um único tipo de dispositivo ou no
máximo de uma classe de dispositivos semelhantes.

O driver recebe das "camadas" acima dele uma solicitação abstrata em uma forma
padronizada e "traduz" esta solicitação nas instruções necessárias para acessar
o dispositivo. Estas instruções em geral consistem em passar os comandos certos
nos registradores da controladora do dispositivo e possivelmente programar a
controladora de DMA para operações que envolvam a memória. Finalmente, o driver
pode ter que esperar o dispositivo concluir sua operação ou em alguns casos a
operação é instantânea, não sendo preciso que o driver seja bloqueado enquanto
espera.

O subsistema de E/S
====================

Esta é a parte independente de dispositivos do SO. Ela vai tratar das operações
de E/S independentemente dos "detalhes" de cada driver.

**Escalonamento de E/S:** Consistem em cuidar da ordem em que os pedidos devem ser
executados, buscando melhor o desempenho das operações de E/S e reduzir o tempo
de espera. Por exemplo: a ordem em que os pedidos de leitura de um disco são
feitos pode ser rearranjada de forma a minimizar os movimentos da cabeça de
leitura/gravação do disco.

**Buffer:** Como a velocidade de transferência entre a CPU e o dispositivo, ou entre
dispositivos pode ser muito diferente, convém armazenar temporariamente os dados
transferidos na memória. Esta técnica chama-se buffering. Os dados são lidos de
um dispositivo e colocados no buffer até que ele fique cheio. Então o outro
dispositivo pode ler um "buffer" inteiro de uma vez, o que é mais eficiente do
que aguardar o dispositivo original receber ou enviar os dados diretamente.

**Cache:** O cache é uma região de memória rápida que armazena cópias de dados. Por
exemplo: se um determinado arquivo em disco é acessado com muita frequência é
mais eficiente manter uma cópia dele na memória e acessá-la sempre que for
necessário carregar aquele arquivo.

**Spool:** Um spool é um tipo de buffer que armazena saída para um dispositivo, como
uma impressora ou uma unidade de fita, que não podem acessar fluxos de dados
intercalados. Dois processos não podem "imprimir" seus dados simultaneamente,
mesmo porque a saída resultante não seria útil em nenhum dos casos. Neste caso,
toda saída para impressora é redirecionada para um arquivo em disco e colocada
em uma fila de espera. Um módulo do kernel (ou mesmo um processo de usuário em
alguns sistemas) irá imprimir estes arquivos um de cada vez. Isto permite que
vários processos possam submeter documentos a serem impressos simultaneamente,
embora cada solicitação seja atendida separadamente.

Tratamento de pedidos de E/S
============================

- Processo de usuário
- Subsistema de E/S
- Driver de dispositivo
- Controlador de interrupções
- Hardware

Exemplo do tratamento de uma leitura de um arquivo armazenado em algum
dispositivo:

1. O processo do usuário faz a chamada de sistema requisitando a leitura de um
arquivo já aberto.
2. O SO verifica se os parâmetros são válidos e em seguida verifica se o
arquivo já não está disponível no cache do sistema. Se estiver, os dados são
transferidos para o buffer do processo e a operação é concluída.
3. Caso contrário, uma operação de E/S é necessária. O processo é colocado na
fila de espera para o dispositivo e o pedido de E/S é escalonado. O pedido é
então "enviado" ao driver de dispositivo.
4. O driver de dispositivo aloca um buffer na memória do kernel e transforma as
solicitações do sistema de E/S em comandos para a controladora.
5. A controladora do dispositivo opera o hardware para fazer a transferência
dos dados.
6. O driver pode fazer E/S programada (PIO) ou programar a controladora de DMA
para fazer a transferência dos dados, que quando concluída, será sinalizada com
uma interrupção.
7. Quando a operação é concluída, uma interrupção é gerada e o tratador de
interrupções passa o controle para o driver.
8. O driver determina qual pedido de E/S foi concluído e avisa o subsistema de
E/S.
9. Este copia os dados do buffer do kernel para o espaço de memória do processo
e o move da fila de espera para a fila de processos prontos.
10. O processo volta da execução da chamada de sistema e a operação de leitura
foi concluída.


Questionário
============

1. Dê um exemplo de dispositivo de bloco e um dispositivo de caractere.

2. Pra que serve um driver?

3. Explique a diferença entre buffer, cache e spool.

4. O que faz o subsistema de E/S?
