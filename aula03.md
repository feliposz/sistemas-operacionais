Visão geral dos sistemas de computação
======================================

~~~
CPU -> Barramento -> Controlador de dispositivo -> Dispositivo
~~~

**Controlador de memória:** A CPU e os diversos dispositivos podem acessar a memória
concorrentemente.

**Inicialização:** POST (Power On Self Test), Bootstrap program (boot), carregamento
do kernel e inicialização. Execução do primeiro processo (init, no Linux) e logo
em seguida aguarda eventos (interrupções, erros e chamadas de sistema).

Existe um documento que descreve detalhadamente o processo de inicialização do
Linux.
<http://www.tldp.org/HOWTO/From-PowerUp-To-Bash-Prompt-HOWTO.html>

**Tratamento de interrupção:** CPU desvia para um ponto fixo que contém o código
responsável por tratar da interrupção e retorna em seguida.

A interrupção deve salvar o estado do processador (registradores, flags, etc) e
restaurá-lo depois de sua execução para que o processo executado anteriormente
volte a rodar como se nada tivesse acontecido.

Os SOs modernos são baseados em interrupções. Se nada acontecer, o SO ficará
parado, esperando.


Estrutura de E/S
================

Cada controladora trata de um tipo de dispositivo, podendo tratar mais de um
dispositivo em alguns casos. Ela é responsável pela passagem dos dados do
dispositivo e controle do seu próprio "buffer local".

**Entrada e saída programada (PIO):**<br>
O SO fica verificando constantemente (polling) se um determinado dispositivo
concluiu sua operação.

**Interrupções de E/S:**<br>
O SO "manda um sinal" para a controladora iniciar uma operação. Esta inicia a
operação solicitada e quando termina gera uma interrupção. Quando o SO recebe a
interrupção ele deve se encarregar de copiar os dados do buffer da controladora
para a memória principal. Em geral essa operação ocorre quando um programa ou um
usuário solicitam entrada e saída.

**Acesso direto à memória (DMA):**<br>
Usado para dispositivos de alta velocidade. O DMA é capaz de transferir grandes
quantidades de dados de/para a memória sem interromper o processador, exceto
quando a operação termina.


Estrutura de armazenamento
==========================

Memória principal
-----------------

Os programas precisam estar na memória para serem executados. A memória
principal (além dos registradores) é a única área de armazenamento a que o
processador tem acesso diretamente. Os dados e as instruções dos programas são
armazenados na memória.

Seria ideal manter sempre todos os programas a serem executados na memória
principal, mas esta em geral é pequena demais para armazenar todos os programas
e dados permanentemente além de ser volátil. Sendo assim, a maioria dos sistemas
fornece armazenamento secundário como uma extensão da memória principal.

Discos magnéticos
-----------------

O dispositivo de armazenamento secundário mais comum é o disco magnético. A
maior parte dos programas é armazenada em disco até ser carregado na memória e
muitos usam os discos como origem e destino de seus dados, tornando a gerência
de discos um dos aspectos mais fundamentais do SO.

Exemplos:
Disco rígido, Disquetes, Discos magnéticos removíveis (Zip/Jaz)

Fitas magnéticas
----------------

Já foi usada como um meio inicial de armazenamento secundário. Embora seja
relativamente permanente e possa armazenar grandes quantidades de dados, seu
tempo de acesso é bem mais lento que o dos discos rígidos, sendo que em geral
são usadas apenas para cópias de segurança (backup) ou para transferir grandes
quantidades de dados entre computadores.

Hierarquia de armazenamento
===========================

~~~
↑ Velocidade e custo maiores ↑
    1 registradores
    2 cache
    3 memória principal
    4 "disco eletrônico"
    5 disco magnético
    6 disco ótico
    7 fitas magnéticas
↓ Velocidade e custo menores ↓
~~~

Cache
-----

O acesso aos registradores podem ser feitos na base de uma ou mais operações por
ciclo de clock, enquanto o acesso à memória principal é na velocidade do
barramento (bem mais lenta) sendo que o processador teria que aguardar cada vez
que acessa a memória. Como a memória é utilizada frequentemente esta espera é
intolerável. A solução é acrescentar uma memória intermediária mais rápida
(cache) para acomodar esta diferença de velocidade.

O caching consiste no seguinte. Antes de buscar uma determinada informação na
memória, verificamos se ela está disponível no cache (que é muito mais rápido).
Se a informação estiver lá, não é preciso buscá-la na memória, caso contrário é
só copiar as informações da memória principal para o cache e todos os acessos
subsequentes poderão consultar a informação no cache, sem precisar buscar na
memória.

A memória principal pode ser considerada um "cache" para o armazenamento
secundário, já que os programas devem ser lidos na memória antes de serem
executados e os dados devem estar na memória param serem gravados em disco.

Coerência e consistência
------------------------

Garantir que os dados em cache sejam atualizados corretamente de/para a memória
é fundamental. A situação começa a complicar quando se tem vários processos
acessando a mesma região da memória, depois vários processadores (sistemas
paralelos). Isto é tratado em nível de hardware, independentemente do SO. Ainda
existe a necessidade de consistência destas informações entre sistemas
distribuídos. Neste caso a responsabilidade é do SO Distribuído.


Proteção de hardware
====================

A princípio os sistemas de computação eram operados por um único usuário e este
tinha controle total do SO. Se algum problema ocorresse durante a operação de um
programa, apenas este seria afetado.

À medida que os SOs se desenvolveram eles passaram a controlar e monitorar uma
série de funções que antes eram de responsabilidade do programador. Para
melhorar a utilização do sistema, o SO passou a compartilhar recursos -
inclusive memória e CPU - para que vários programas pudessem ser executados
simultaneamente.

Embora o compartilhamento tenha melhorado a utilização, ele também aumentou os
problemas. Um erro em um programa poderia causar falhas em outros programas
sendo executados ao mesmo tempo. O SO deve cuidar para que erros em um programa
não afetem a execução dos outros programas.

Operação em modo dual
---------------------

A abordagem mais usada para garantir a operação do sistema é termos vários
níveis ou modos de operação. São necessários ao menos 2: modo usuário e modo
monitor (ou supervisor, sistema, privilegiado). Sendo assim, algumas tarefas
passam a ser executadas apenas pelo sistema operacional, quando em modo monitor.
No modo usuário certas operações passam a ser proibidas.

Sempre que a operação passar para o SO (e também na inicialização) o sistema
passa para o modo monitor. Quando a execução voltar a executar os processos
comuns, o modo usuário é ativado.

Este modo dual protege o SO dos usuários e os usuários uns dos outros.

Sistemas como o MS-DOS, projetados para as CPUs 8088 da Intel não tinham essa
capacidade de modo de operação dual, o que permitia que qualquer programa
pudesse alterar o SO durante a operação (daí a facilidade de criação e a
diversidade de vírus para tal sistema). A partir do processador 80386 essa
capacidade foi incluída e os sistemas operacionais mais recentes (Windows NT,
OS/2) puderam tirar proveito desta proteção para o SO.

**Proteção de E/S:**<br>
Processos errantes podem perturbar o sistema emitindo operações de E/S ilegais.
Para evitar isto, trata-se toda operação de E/S como privilegiada, sendo que
todo programa deve passar pelo SO para executar tais operações.

**Proteção de memória:**<br>
Para evitar que um processo altere dados (ou mesmo código) na memória de outros
processos ou até do próprio SO é preciso delimitar o espaço de memória a que o
processo tem direito. Todo processador moderno oferece esse tipo de proteção. Só
o modo monitor possui acesso irrestrito à toda memória.

**Proteção de CPU:**<br>
Para evitar que um processo "guloso" tome todo o tempo da CPU do sistema (num
laço infinito, por exemplo) utiliza-se um timer (temporizador) que interrompe o
processador periodicamente (a cada 1/100 de segundo por exemplo). Antes de
passar a execução para um processo, o SO delimita um determinado tempo para sua
operação. Se o processo não termina sua operação durante esse tempo uma
interrupção é gerada pelo timer e o controle volta para o SO. Além disso o timer
é usada para fazer o compartilhamento de tempo. Quando o controle é devolvido ao
SO, este pode escolher outro processo para ser executado no lugar do que foi
interrompido e assim por diante. Para fazer esta troca, uma série de informações
referentes a cada processo deve ser controlada. Esta troca de execução de um
processo para outro é chamada de "troca (ou mudança) de contexto".


Arquitetura geral do sistema
============================

- Modo dual: instruções privilegiadas que só o SO pode executar
- Os programas de usuário devem solicitar tais operações ao SO, que tem acesso e
controle sobre elas. Tais solicitações recebem o nome de **chamadas de sistema**.


Questões para estudo
====================

1 - Qual a função do programa de inicialização (bootstrap program)?

2 - Cite alguns tipos de controlador de dispositivo que você conhece.

3 - Qual a vantagem do uso do DMA sobre o modo PIO (entrada e saída programada)?

4 - A CPU é capaz de acessar os dispositivos diretamente? É possível executar
diretamente um programa armazenado em disco ou fita?

5 - Faça uma pesquisa rápida de preços, visando obter a relação MB/R$ para os
seguintes dispositivos: Memória RAM, Disco rígido, CDs e Fitas magnéticas

6 - Por que é necessário o uso de cache? A memória principal já não é rápida o
bastante?

7 - Na operação em modo dual, os programas de usuário estão proibidos de fazer
certas operações. Quais destas operações devem ser permitidas para o modo
usuário e quais apenas para o modo monitor (SO):

- [ ] Acesso à própria memória
- [ ] Acesso à memória de outros processos
- [ ] Controlar as interrupções do sistema
- [ ] Fazer chamadas ou solicitações ao sistema operacional
- [ ] Acesso direto aos dispositivos de E/S
- [ ] Usar todo o tempo de CPU que for necessário

