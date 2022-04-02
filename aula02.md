Tipos de Sistemas Operacionais
==============================

Antes dos SOs
-------------

Hardware:
- Computadores enormes com tubos de vácuo e programação feita diretamente na
placa de circuitos
- Qualquer computador atual é centenas ou milhares de vezes mais rápido que
estas máquinas

Aplicativos:
- Programas eram criados conectando-se plugs e cabos em placas que eram
conectadas ao sistema de computação
- A maioria dos programas

SO:
- Não haviam SOs

Usuário:
- O sistema precisava de uma equipe de operadores e técnicos dedicados a cuidar
de todo aspecto de funcionamento do sistema

Sistemas em lote (batch)
------------------------

Hardware:
- Computadores grandes (fisicamente) e caros, trancados em salas especiais com
ar-condicionado
- Entrada: Cartão e fitas
- Saída: Impressoras, gravadores de cartão e perfuradores de fita
- Sem interação direta do usuário
- Começou a se tornar viável comercialmente o uso de computadores

Aplicativos: 
- Programas eram executados submetendo-se tarefas na forma de um
programa e instruções de controle (indicando entrada e saída de dados, por
exemplo). 
- O programa era lido dos cartões perfurados, e após algum tempo
(minutos, horas ou dias) produzia uma saída e encerrava sua execução,
possivelmente com um "dump" (despejo) de memória e conteúdo dos registradores no
caso de um erro.

Sistema Operacional: 
- Simples, sua função era transferir o controle
automaticamente de uma tarefa (job) para a próxima.

Usuário: 
- Os programadores passavam seus programas para um operador que reunia as
tarefas (Jobs) com requisitos semelhantes em um lote (daí o nome) para aumentar
a eficiência e as saídas (impressas ou perfuradas em cartão) eram enviadas de
volta aos programadores.

Características:
- CPU Ociosa (muito tempo em E/S e pouco tempo processando devido à diferença na
velocidade)
- Para economizar o tempo de carregamento dos cartões e o tempo desperdiçado
imprimindo as saídas, o carregamento era feito em uma máquina de menor
capacidade e gravado em fita magnética que era então processada pelo equipamento
mais caro que por sua vez gerava sua saída em outra fita. Esta fita era então
lida por outro equipamento de menor capacidade que cuidava da impressão.

Multiprogramação (multi-programming)
----------------

- Com a introdução da tecnologia de discos tornou-se possível submeter diversas
tarefas simultaneamente aos sistemas de computação. Várias tarefas poderiam ser
armazenadas em disco e o sistema operacional poderia, se fosse multiprogramado,
carregar várias delas simultaneamente na memória. Desta forma, quando um
programa solicitasse E/S e ficasse esperando, o SO poderia passar o controle
para outro programa e assim sucessivamente, de forma que, enquanto houver ao
menos um programa pronto para usar a CPU, esta não ficará ociosa.
- Os SOs multiprogramados eram bem mais sofisticados do que os sistemas em lote
comuns, pois teria que tomar decisões sobre qual tarefa executar primeiro,
controlar E/S e tempo de CPU, espaço de memória, etc.

Sistemas de tempo compartilhado (time-sharing)
-------------------------------

Necessidade:
- Apesar dos sistemas de multiprogramação serem úteis para processamento
científico intenso e processamento de dados comerciais em massa, eles
continuavam sendo sistemas em lote. O tempo entre submeter uma tarefa e esperar
seu resultado poderia ser de horas.
- Programadores desejavam respostas rápidas do sistema. Um único erro de
compilação poderia significar para o programador perder metade do dia.

Características
- Os sistemas de tempo compartilhado são uma variação dos sistemas de
multiprogramação em que cada usuário tem um terminal ligado ao sistema.
- Os programadores em geral executam tarefas pequenas (ex: compilar uma rotina
de 5 páginas) em comparação com tarefas de usuários (ex: ordenar um arquivo de
um milhão de registros) que podem ser processados imediatamente enquanto as
tarefas mais demoradas podem ser executadas em segundo plano (background).

Histórico:
- O primeiro sistema (CTSS) foi desenvolvido pelo MIT mas não se tornou popular
devido à falta de hardware para proteção
- O MULTICS foi um projeto do MIT, Bell Labs (AT&T) e General Electric para
criar um sistema que pudesse comportar centenas de usuários simultâneos.
- O MULTICS foi um projeto ambicioso demais para a época e acabou fracassando,
mas conceitos dele são aplicados até hoje.
- Um dos engenheiros que trabalharam no MULTICS (Ken Thompson) escreveu uma
versão simplificada deste para um único usuário que posteriormente tornou-se o
Unix.
- O Unix ganhou aceitação rapidamente pois tinha seu código aberto e acabou se
desenvolvendo em uma série de SOs incompatíveis entre si. Esta incompatibilidade
fez com que diversos padrões fossem desenvolvidos, sendo que o mais popular (e
que a maioria dos sistemas suporta) é o POSIX.

Sistemas de computadores pessoais (PC, personal computer)
---------------------------------

- Enquanto a introdução dos mini-computadores tornou possível que um
departamento em uma empresa ou universidade tivesse seu próprio computador, o
microprocessador tornou possível que cada usuário tenha seu próprio computador.
- Computadores baratos e produzidos em massa.
- Diversas empresas produzindo software para uso pessoal, com características
"amigáveis"
- Uma Workstation (Estação de trabalho) é basicamente um PC mais poderoso.

Inicialmente dois sistemas foram dominantes na área de computação pessoal: o MS-
DOS e o Unix. O DOS em PCs e o Unix em Estações de trabalho.

- O DOS dominou rapidamente a arquitetura x86 sendo que suas primeiras versões
eram muito primitivas, posteriormente incorporando algumas características do
Unix. O Windows era inicialmente um programa que rodava sobre o DOS, sendo que
apenas após 1995 passou a ser um SO independente. O Windows NT, embora apresente
semelhança e certa compatibilidade com o o Windows 95/98, é um sistema operacional
totalmente diferente, reescrito do zero.

- O Unix por outro lado tornou-se especialmente popular para uso em estações de
trabalho e servidores de rede, máquinas geralmente equipadas com processadores
RISC de alta-performance.

Sistemas paralelos
------------------

- Fortemente acoplados.

- Sistemas multiprocessador, onde mais de um processador compartilha o
barramento, o clock e às vezes a memória e os dispositivos periféricos.
- Objetivo é aumentar a taxa de produção (throughput), onde espera-se obter N
vezes mais capacidade de processamento onde existirem N processadores.
- Economia com hardware e periféricos em relação a vários sistemas com um
processador cada.
- Tolerância a falhas (se um processador falhar a operação é distribuída entre
os restantes, sem a necessidade de parar o sistema).
- Multiprocessamento simétrico - todos os processadores executam cada um uma
cópia do SO comunicando-se conforme necessário.
- Multiprocessamento assimétrico - um processador mestre controla os outros que
são "escravos" e aloca trabalho para eles.
- Praticamente todos os SOs modernos fornecem algum tipo de suporta a
multiprocessamento: Windows NT, Solaris, Unix, OS/2, Linux, etc.

- Multiprocessamento que não é multiprocessamento? Controlador de disco,
teclado, etc.

Sistemas de tempo real (real-time)
----------------------

- Requisitos rígidos de tempo de resposta. O processamento deve ser feito DENTRO
do limite de tempo fixada ou o sistema falhará.
- Exemplos: controle de máquinas, alguns eletrodomésticos, injeção de
combustível em motores de veículos, armamento
- Comparação:
  - em SO de tempo compartilhado é _desejável_ que a resposta seja rápida
  - em SO em lote não há limitação de tempo
- Crítico:
  - Todos os atrasos são limitados
  - Recursos avançados do SO estão ausentes (separação do hardware, memória
  virtual, etc)
  - Conflito com os sistemas de tempo compartilhado
- Não-crítico:
  - Menos restrito
  - Uma tarefa crítica recebe a mais alta prioridade até ser concluída
  - Utilidade mais limitada para aplicações críticas como controle industrial e
  robótica
  - Pode ser encontrado suporte nos principais Unix e no Windows NT

Sistemas distribuídos
---------------------

- Fracamente acoplados.

- Sistema operacional de rede: vários computadores conectados em rede
compartilhando recursos (impressoras, sistemas de arquivo, etc). Cada computador
atua de forma independente apenas trocando mensagens entre os componentes da
rede. O sistema operacional de rede é o próprio SO mais um módulo que controla
sua comunicação com outras máquinas.
- Sistema operacional distribuído: nestes sistemas toda a rede forma um único
sistema, sendo que se tem a impressão de que há um único computador fazendo o
processamento.


Questões para estudo
--------------------

1) Qual a principal vantagem da multiprogramação?

2) Faça um comparativo entre as características dos sistemas operacionais para
mainframes e SOs para uso em computadores pessoais.

3) Descreva brevemente o que é:

- Um sistema em lote (batch)
- Um sistema de tempo compartilhado (time-sharing)
- Um sistema paralelo
- Um sistema de computadores pessoais (PC)
- Um sistema de tempo real
- Um sistema operacional de rede
- Um sistema operacional distribuído

