Arquitetura de Sistemas Operacionais
====================================

Componentes do SO
-----------------

**Gerenciador de processos:**

Em uma definição geral, um processo é um programa em execução (um compilador, um
processador de textos, etc). Cada processo precisa de certos recursos para ser
executado (CPU, Memória, Arquivos e Dispositivos de E/S). O processo é a unidade
de trabalho de um sistema de computação e tais sistemas possuem processos do SO
e do usuário sendo executados. As funções do SO com relação aos processos são:
criar, excluir, suspender e retomar processos; fornecer mecanismos para
sincronização e comunicação entre os processos; tratar deadlocks.

**Gerenciador de memória:**

Para que um programa seja executado, ele precisa ser carregado na memória e ser
mapeado com endereços de memória absolutos. Conforme ele é executado, fará
referência a estes endereços e por fim, quando termina, a memória alocada para
ele deve ser liberada. Para fazer uso eficiente do sistema, diversos processos
devem ser carregados na memória para execução. Há várias formas de fazer isso
dependendo de diversos fatores (inclusive suporte do hardware). Funções do SO
com relação à memória: manter uma relação de quais partes da memória estão sendo
usadas e por quais processo, decidir quais processos devem ser carregados na
memória se houver espaço, alocar e desalocar espaço, conforme necessário.

**Gerência de arquivos:**

Os dispositivos de armazenamento possuem uma série de propriedades particulares
(velocidade e método de acesso, taxa de transferência, etc). A função da
gerência de arquivos do SO é prover um meio lógico e uniforme, para que os
processos e usuários possam lidar mais facilmente com tais particularidades. O
conceito de arquivo (e o sistema de diretórios) é uma forma de mapear as
unidades físicas para conceitos lógicos que tornam seu uso mais fácil. Ainda é
função do SO controlar os direitos de acesso a tais arquivos. Funções do sistema
de arquivos: criar, excluir e fornecer outros meios de manipular arquivos e
diretórios; mapear arquivos nos meios de armazenamento secundários; permitir um
meio de se fazer backup dos arquivos e meios não-voláteis.

**Sistema de Entrada e Saída:**

É função do SO esconder as peculiaridades dos dispositivos de E/S. O subsistema
de E/S consiste em: um componente da gerência de memória responsável por
buffering, cache e spooling; uma interface geral de drivers; os drivers
específicos para cada dispositivo.

**Gerência de Armazenamento Secundário:**

Como a memória principal é volátil (e limitada) é preciso uma forma de armazenar
permanentemente arquivos de dados e de programas.  A gerência de armazenamento
secundário é responsável por: gerenciar espaço livre, alocar espaço, escalonar o
acesso ao disco.

**Redes:**

Os computadores podem ser ligados em redes de diversos níveis de complexidade e
é função do módulo de redes de um SO, permitir que os sistemas se comuniquem e
que o processamento seja distribuído adequadamente.

**Proteção:**

Em um sistema onde vários usuários e processos podem trabalhar simultaneamente,
deve-se garantir que um não interfira na operação do outro, protegendo-se o
espaço de memória, evitando que um processo controle a CPU indefinidamente e
controlando o acesso aos diversos recursos, permitindo-se que somente os
usuários autorizados façam uso dos mesmos.

**Interpretador de comandos:**

É um dos módulos mais importantes, chegando a definir a "aparência" do sistema
para o usuário final. O interpretador de comandos (ou shell) pode ser uma parte
do próprio núcleo do sistema operacional, ou um processo separado. Sua função é
receber comandos do usuário, que definem o que deve ser feito pelo SO para
cumprir uma determinada tarefa. A forma como ele funciona, pode variar desde um
programa que lê uma série de informações de controle de jobs a partir da
entrada; passando por um complexo sistema onde se digita comandos com parâmetros
em um prompt; até um sistema completamente gráfico, onde se utiliza um
dispositivo apontador para tratar dos processos, arquivos e demais recursos,
que são todos representados graficamente como "ícones" e "janelas".


Serviços do SO
--------------

-  Execução de Programas: Carregar o programa na memória, executar e encerrar
sua execução (possivelmente, podendo indicar algum erro)

- Operações de E/S: Acesso a arquivos ou dispositivos de E/S que não podem ser
acessados diretamente pelos usuários e processos (por questões de segurança e
eficiência.

- Manipulação do Sistema de Arquivos: Criar, excluir, ler e gravar arquivos.

- Comunicação: Troca de mensagem entre processos ou memória compartilhada.

- Detecção de Erros: O SO deve detectar e tratar adequadamente os erros de
hardware, memória, nos dispositivos, nos programas de usuário, etc.

- Alocação de Recursos: Em sistemas com múltiplos usuários e processos, é
preciso controlar quem vai acessar cada recurso e reservá-lo, para que outros
processos e usuários não interfiram na sua execução.

- Contabilização: Registrar os recursos que são utilizados por usuário é
importante para contabilização ou mesmo para fornecer estatísticas a serem
usadas para otimizar o sistema.

- Proteção: Evitar que processos interfiram na execução um do outro, assim como
o acesso não autorizado ao sistema ou recursos do mesmo.


Chamadas de Sistema
-------------------

Chamada de Sistema é o mecanismo pelo qual os processos de usuário tem acesso
aos serviços do SO. Em geral são implementadas na forma de instruções em
linguagem assembly, mas comumente podem ser acessadas através de linguagens de
alto nível (C, C++, Perl, Delphi, etc). A maior parte da complexidade do uso das
chamadas de sistema está "escondida" nas rotinas das bibliotecas de sistema,
sendo que a maior parte dos usuários e programadores jamais fará uso direto
delas.

Tipos de chamadas de sistema:

- Controle de processos: criar, carregar, executar e terminar; pegar e alterar
atributos; sinalizar ou esperar um evento; alocar e liberar memória.

- Manipulação de arquivos: criar, apagar, abrir, fechar, ler e gravar; pegar e
alterar atributos do arquivo.

- Manipulação de dispositivos: reservar e liberar dispositivos; ler, gravar e
reposicionar; conectar ou desconectar logicamente.

- Manutenção de informações: ler e alterar  informações como data e hora, dados
do sistema, atributos de processos, arquivos e dispositivos.

- Comunicação: criar e apagar conexões de comunicação; enviar e receber
mensagens e informações de status; conectar ou desconectar dispositivos remotos.


Programas de Sistema
--------------------

Um sistema de computação é formado por hardware, sistema operacional, programas
de sistema, e aplicativos do usuário. Os programas de sistema fornecem um
ambiente conveniente para o desenvolvimento e execução de programas. Categorias:

- Gerência de arquivos: cria, excluir, copiar, renomear, imprimir, listar e
manipular arquivos e diretórios.

- Informações de status: programas que pedem ao sistema informações gerais e as
exibem, tais como: data, hora, quantidade de memória e espaço em disco,
usuários, etc.

- Modificação de arquivo: diversos tipos de editores de texto.

- Suporte à linguagem de programação: compiladores, montadores e interpretadores
para linguagens de programação. A maior parte destes programas agora são
distribuídos separadamente, geralmente de forma paga.

- Carregamento e execução de programas: utilitários de carga, link-editores,
sistemas de depuração (alto nível e linguagem de máquina).

- Comunicação: programas para criar conexões remotas com processos em outros
computadores. Exemplos: FTP, navegadores Web, correio eletrônico, etc.


Estrutura do sistema operacional
--------------------------------

**Estrutura simples:**

Sistemas que não possuem uma estrutura bem definida, sendo que os diversos
módulos do kernel estão "misturados" num único programa. Em sistemas com o MS-
DOS, nem mesmo o hardware era separado dos programas de usuário, sendo que os
programas poderiam ter acesso direto aos dispositivos do sistema. O Unix
original sofria de problemas semelhantes devido à falta de suporte de hardware,
que foi implementado depois, permitindo um melhor controle do SO sobre a
máquina.

**Estrutura em camadas:**

Uma das formas de modularizar um sistema é através de camadas, sendo que cada
uma é construída sobre as outras e possui níveis de acesso diferentes. As
camadas inferiores são construídas de forma a prover serviços convenientes às
camadas acima. As camadas superiores fazem uso das camadas mais baixas, sem nem
precisar "saber" como os serviços são implementados. Neste tipo de projeto a
implementação e depuração do sistema é mais simples. No entanto, alguns
problemas surgem, como performance reduzida e dificuldade ao definir as funções
das camadas.

**Microkernel:**

No modelo de microkernel, todos os serviços não-essenciais do sistema
operacional são removidos do kernel e passam a ser executados no modo usuário. O
microkernel faz então apenas o controle de processos e memória, sendo que outros
serviços como sistema de arquivo, entrada e saída, etc, são executados por
processos do SO que executam com privilégio de usuário. As vantagens são que o
sistema é mais fácil de expandir (um novo módulo pode ser acrescentado sem
alterar o kernel), mais robusto (uma falha em algum módulo não resultará numa
pane geral, já que apenas o microkernel roda em modo protegido) e facilidade ao
portar para outros sistemas (já que apenas o kernel precisa ser adaptado na
maioria dos casos).

Máquina virtual
---------------

Num modelo de máquina virtual, a abordagem em camadas é levada ao extremo. O SO
de máquina virtual usa técnicas de escalonamento de CPU e memória virtual para
simular diversas "instâncias" de uma máquinas virtuais. Cada uma delas é uma
cópia exata do Hardware original, sendo que os programas podem ser executados
como se estivessem rodando no próprio hardware. É possível inclusive executar
Sistemas Operacionais diferentes e cada uma das máquinas virtuais, sendo que
cada uma está totalmente isolada das outras.

**Máquina virtual Java:**

Java é uma tecnologia e não apenas uma linguagem de programação. Ela fornece 3
itens: a linguagem de programação, a interface de programação de aplicações
(API), a máquina virtual Java.

A máquina virtual Java consiste num computador abstrato sobre os quais são
executados os programas criados na linguagem Java e compilados em "bytecode" que
são os códigos (instruções) para essa máquina virtual. A máquina virtual então
"interpreta" este código, executando o programa. A vantagem deste modelo é que a
máquina virtual torna os programas totalmente independente de hardware, pois uma
determinada aplicação, uma vez compilada, pode rodar em qualquer máquina virtual
Java, não importa em que arquitetura. Os detalhes dependentes da máquina e do
sistema operacional, são tratados por cada implementação da máquina virtual
Java.


Questionário
============

1) Cite três módulos do SO que você considera importante e descreva
resumidamente a função deles.

2) Qual o objetivo do interpretador de comandos?

3) Por que é função do sistema operacional alocar recursos para os processos?
Por que estes não podem acessá-los diretamente?

4) O que é uma chamada de sistema?

5) Cite 3 exemplos de programas de sistema de algum sistema operacional que você
conhece e qual a função de cada um deles.

6) Compare as estruturas de microkernel e estrutura simples (monolítica).
