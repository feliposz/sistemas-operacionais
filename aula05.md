Processos
=========

Processo e Job
--------------

Podemos definir processo como sendo um programa em execução, seja ele um
programa de sistema (um módulo do sistema operacional) ou um programa do
usuário. A palavra "job" é usada para designar um processo submetido para
execução num sistema em lote. Já em sistemas de tempo compartilhado podemos
chamá-los de tarefas ou apenas "programas do usuário".

Um sistema é justamente uma coleção dos processos de sistema e de usuário sendo
executados, sendo que este sistema pode ser multiprocessado (isto é, tem a
capacidade de executar mais de um processo simultâneo).

O Processo
----------

Um processo consiste em seu próprio código sendo executado (também chamado de
seção de texto) e mais uma série de informações da atividade corrente: contador
de programa, registradores da CPU, sua própria pilha e a seção de dados, onde
estão as variáveis globais do programa.

Conforme o processo é executado e efetua suas operações ele passa por diversos
estados: Novo, Em execução, Em espera, Pronto, Encerrado.

Cada processo é representado no SO por um Bloco de Controle de Processo (PCB)
que é composto das seguintes informações: Estado do processo, Contador do
programa, Registradores de CPU, Informações de escalonamento de CPU, de gerência
de memória, de contabilização e de E/S.

Escalonamento de processos
--------------------------

É objetivo da multiprogramação ter processos executando o tempo todo. O objetivo
do tempo compartilhado é alternar a CPU entre os processos rapidamente passando
a ilusão de que todos são executados simultaneamente.

**Filas (queues) de escalonamento:** À medida que os processos são submetidos para
execução eles são colocados na fila de jobs. Quando um processo é escolhido para
execução ele passa para a fila de processos prontos e fica aguardando sua vez de
usar a CPU. Se um processo precisa esperar por um determinado dispositivo (o
disco por exemplo) ele é colocado na fila de espera daquele dispositivo e deve
esperar sua vez para poder voltar a ser executado.

**Escalonadores (schedulers):** O escalonador de longo prazo é quem faz a escolha
de qual job deve ser executado. Num sistema em lote os processos aguardam sua
execução num dispositivo de armazenamento de massa até serem carregados na
memória para execução. O escalonador de curto prazo (ou de CPU), seleciona
dentre os processos que estão carregados na memória, qual deve ser executado.

A principal distinção é a frequência de execução. O escalonador de curto prazo
por exemplo, pode executar uma vez a cada 100 milissegundos, enquanto o de longo
prazo pode executar de minuto em minuto.

O escalonador de curto prazo deve ser rápido e eficiente para não tomar dos
processos tempo de processamento. O escalonador de longo prazo controla a carga
de multiprogramação. Alguns programas fazem muita E/S, enquanto outros usam mais
a CPU e o escalonador deve cuidar de qual entra primeiro.

Em alguns SOs existe ainda o escalonador de médio prazo, que pode retirar da
memória (e da disputa pelo processador) um processo em espera e colocá-lo em
disco, liberando espaço para outros processos.

**Troca de contexto:** Para alternar entre os processos é preciso salvar a
situação atual do processo e restaurá-la depois para devolver-lhe o controle.
Esta operação é chamada de troca de contexto. O contexto do processo é
representado no Bloco de Controle de Processo (PCB). A troca de contexto pode
ser potencialmente "demorada" em termos de processamento, dependendo também do
hardware para sua eficiência.  Se o SO alternar muito frequentemente entre os
processos, pode acabar perdendo muito tempo com esse "overhead" e menos tempo
executando os processos em si, e se alternar pouco, reduz o tempo de resposta do
sistema.

Operações
---------

**Criação:** Uma processo (denominado pai), é capaz de efetuar uma chamada de
sistema para criar outros processos (filhos) e este por sua vez pode criar seus
próprios processos filhos, numa estrutura "em árvore". Depois que o processo pai
cria um processo filho ele pode continuar executando normalmente ou pode esperar
que algum dos seus filhos (ou todos) terminem.

**Término:** O término de um processo é feito através da chamada "exit". Os recursos
do processo (memória, arquivos abertos, etc), são desalocados. Um processo pode
terminar de forma anormal, devido a algum erro e neste caso com uma chamada de
sistema diferente (abort).

**Comunicação entre processos (IPC):** O SO fornece mecanismos para que os processos
possam se comunicar. O mais simples é memória compartilhada, onde um espaço de
memória definido pode ser usado por mais de um processo. Neste caso o
programador é responsável por controlar o uso da memória compartilhada. O SO
também fornece um mecanismo para trocar mensagens entre os processos. Essas
mensagens podem ser sincronizadas ou não (por exemplo, o emissor pode ou não ser
bloqueado até que o receptor receba a mensagem, e o receptor pode ficar
bloqueado até receber uma mensagem ou não)

Threads
=======

Thread, também chamado de processo leve, é a unidade básica de execução. Um
processo pode ter um único thread, que consiste num fluxo de execução único, ou
vários threads, cada um com um fluxo de controle independente. Um thread
compreende uma identificação de thread, um contador de programa, conjunto de
registradores e uma pilha. Tal thread, compartilha com os outros threads do
mesmo processo a sua seção de códigos, de dados, arquivos abertos, etc.
Processos com múltiplos threads podem realizar diversas operações
simultaneamente (exemplo: um navegador de internet pode ter um thread para
exibir a página, enquanto outros threads estão carregando arquivos de imagens, e
um outro ainda permite que o usuário interaja com o programa).

Benefícios:
- Capacidade de resposta: Parte da aplicação pode continuar executando
interativamente enquanto outra seção está bloqueada ou executando uma operação
demorada.
- Compartilhamento de recursos: Os threads de um mesmo processo tem acesso à
memória e aos recursos do processo.
- Economia: É mais demorado e mais dispendioso criar um novo processo do que um
novo thread.
- Utilização de arquiteturas multiprocessador: Em sistemas monoprocessados,
apenas um processo (ou mesmo thread) pode ser executado por vez, embora a rápida
alternância entre os processos passe a ilusão de paralelismo. Em um sistema
multiprocessado, os threads, até mesmo de um mesmo processo, podem ser
executados simultaneamente em diversos processadores.

Escalonamento de processos
==========================

O escalonamento de CPU é a base dos sistemas multiprogramados. Alternar a CPU
entre diversos processos torna o computador mais produtivo

Surtos de I/O e CPU
-------------------

Todo processo depende de processamento e E/S. No entanto, a maior parte dos
processos passa apenas uma pequena parte do tempo efetivamente processando e a
maior parte do tempo esperando que operações de E/S sejam efetuadas. Isto
permite que vários processos sejam executados simultaneamente. Enquanto um
processo espera que suas operações de E/S sejam executadas, um outro pode fazer
uso do processador, aumentando a eficiência do sistema.

Escalonador
-----------

**Escalonador de CPU:** Sempre que a CPU fica ociosa, o escalonador de curto prazo,
escolhe um dos processos da fila de processos prontos para ser executado.

**Escalonamento Preemptivo x Cooperativo:** No escalonamento cooperativo, quando um
processo recebe a vez de usar a CPU, ele a mantém até liberá-la, quando o
processamento termina, ou quando deve esperar alguma operação de E/S. No
escalonamento preemptivo, cada processo recebe uma fatia de tempo para usar a
CPU e se não terminou seu processamento, nem entrou em estado de espera, ele é
interrompido e o controle passa para o próximo processo pronto da fila.

**Dispatcher (Despachante):** É o módulo do escalonador responsável pela troca de
contexto entre os processos, por passar o controle para o modo usuário e por
retornar o controle para a posição adequada do processo.

Critérios de escalonamento:
- **Utilização de CPU:** Deve ficar o mais ocupada possível (próxima de 100%). Na
prática, deve ficar entre 40% (pouco processamento) e 90% (muito processamento)
- **Throughput:** Número de processos completados por unidade de tempo. Ex:
Processos longos podem ser 1 por hora e processos curtos, 10 por segundo.
- **Tempo de retorno:** Tempo levado para executar um processo.
- **Tempo de espera:** Tempo esperando para ser executado.
- **Tempo de resposta:** Tempo que leva para o processo começar a responder ao
usuário.

Algoritmos:
- **First-come, first-served (FCFS):** O primeiro processo a entrar na fila é o
primeiro a ser executado
- **Job mais curto primeiro (SJF):** O processo que será executado mais rapidamente
deve ser executado primeiro.
- **Por prioridade:** Uma prioridade é designada para cada processo e aquele com a
prioridade mais alta é executado primeiro.
- **Round-robin:** Revezamento circular. Cada processo recebe uma fatia de tempo
(quantum) para ser executado. Quando aquela fatia de tempo acabar, o controle
passa para o próximo processo. Usado em sistemas de tempo compartilhado. Se o
quantum for muito baixo, o processador vai passar muito tempo alternando entre
processos. Se for muito alto, perde menos tempo alternando, mas o tempo de
resposta pode cair drasticamente.
- **Múltiplas filas:** Os processos são alocados em diversas filas separadas com
prioridades diferentes. Exemplo: Uma fila para processos de primeiro plano
(interativos) e outra para processos de segundo plano (em lote).
- **Tempo real:** Em sistemas de tempo real críticos, cada processo é submetido com
uma informação limitando o tempo necessário para que seja executado. O SO deve
então aceitar o processo garantindo que este será executado no prazo ou recusá-
lo. Em sistemas não-críticos, os processos de tempo real recebem a prioridade
mais alta e não perdem prioridade com o tempo.

Sincronização de processos
==========================

Condição de corrida
-------------------

Quando dois processos (ou threads) compartilham um mesmo recurso, é possível que
ambos tenham acesso a um destes recursos (uma variável, por exemplo) e façam
alterações numa certa ordem, de forma que um não perceba a alteração do outro e
acabe sobrescrevendo tais alterações. Esta situação é conhecida como **condição de
corrida** (race condition).

Seção crítica
-------------

As condições de corrida em geral ocorrem em pontos bem específicos de um
determinado código, e a solução é permitir que apenas um único processo tenha
acesso aos recursos compartilhados de cada vez, através de um mecanismo de
exclusão mútua. Há várias formas de implementar as seções críticas usando
variáveis de flags, mas elas são difíceis de generalizar para vários
processos/threads e outros tipos de problemas.

Semáforos
---------

Semáforo é um mecanismo do SO que permite implementar as seções críticas de
forma segura. O processo precisa verificar e sinalizar o semáforo ao entrar na
seção crítica e liberá-lo antes de sair. Se um semáforo estiver sinalizado é
porque outro processo está em sua seção crítica e deve então aguardar sua vez.

Deadlocks
=========

Recursos
--------

Um sistema de computação possui um certo número de recursos que são usados pelos
processos (disco, impressoras, dispositivos de E/S, etc). Estes recursos são
alocados pelo sistema operacional aos processos mediante pedidos. Os processos
devem liberar os recursos após o uso. Se um determinado recurso estiver em uso
por outro processo este deve esperar que o recurso seja liberado para poder usá-
lo. Quando dois ou mais processos estão simultaneamente aguardando a liberação
de um determinado recurso um do outro, temos um impasse ou deadlock.

Condições para ocorrer deadlock
-------------------------------

- **Exclusão mútua:** Ao menos um recurso deve estar mantido em modo exclusivo. Outros
processos devem aguardar o recurso ser liberado.
- **Posse e espera:** Deve haver um processo bloqueando um recurso e aguardando outro.
- **Não-preempção:** Os recursos não podem sofrer preempção. Cada recurso só pode ser
liberado pelo processo que o bloqueou quando ele terminar sua tarefa.
- **Espera circular:** No mínimo dois processos devem estar um aguardando o recurso
alocado pelo outro numa espera circular.

Tratamento de deadlocks
-----------------------

1) Podemos garantir que nunca ocorra um deadlock
2) Podemos permitir que um deadlock ocorra e fazer alguma coisa para recuperar a
situação
3) Podemos ignorar o problema completamente, deixando a responsabilidade de
evitar e tratar os deadlocks nas mãos dos programadores

**Prevenção:** Para prevenir deadlocks, uma das condições que resultam em deadlock
devem ser evitadas.

**Impedimento:** A desvantagem do esquema de prevenção é que o sistema pode perder
produtividade. Uma alternativa é fazer com que todos os processos declarem
previamente quais os recursos que vão usar e o SO se responsabiliza por evitar
que o sistema entre em deadlock analisando as ordens dos pedidos.

**Detecção e recuperação:** Como nem sempre é possível determinar com antecedência
exatamente quais recursos um processo vai usar, é possível também permitir que
um deadlock ocorra e então tratá-lo. O SO pode tanto detectar um deadlock e
simplesmente avisar o operador como também recuperar-se automaticamente da
situação. A recuperação consiste ou em terminar um dos processos da espera
circular ou fazer a preempção de um dos recursos bloqueados por um destes
processos.


Questões para estudo
--------------------

1) Quais são as informações de um processo que o SO deve controlar (referentes
ao PCB, bloco de controle de processo) e quais os estados que um processo pode
atingir durante sua execução?

2) Qual a função do escalonador de CPU no SO?

3) O que é troca de contexto? Qual módulo do SO faz a troca de contexto?

4) O que é thread e qual a vantagem do seu uso?

5) Qual é a principal vantagem do escalonamento Round-robin sobre o First-come,
First-served?

6) O que é deadlock e quais as condições para que ele ocorra?
