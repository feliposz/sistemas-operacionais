Sistema Operacional
===================


Objetivos do Sistema Operacional
--------------------------------

- Geral: Fornecer ambiente em que o usuário possa executar programas.
- Principal: Conveniência do usuário (tornar possível executar os programas e
resolver os problemas do usuário)
- Secundário: Eficiência (fazer uso eficiente do Hardware para que este seja
utilizado em todo seu potencial)


Sistema de Computação
---------------------

- Hardware / Arquitetura
    - Exemplos: x86 (Intel, AMD), Macintosh, VAX, Sun, SPARC, Alpha, Mainframe

- Sistema Operacional
    - Exemplos: DOS, Windows (9x, NT, 2000, 2003, XP), Linux, Unix, MacOS, VMS,
Solaris, BSD, OS/2, PalmOS, Windows CE

- Aplicativos
    - Exemplos: Suítes de Escritório (Office, OpenOffice), Browsers, Jogos, CAD,
Agenda

- Usuários
    - Exemplos: Pessoas, máquinas ou outros computadores


O que é um SO?
--------------

- "Governo": Fornece um ambiente mas não "produz" nada de útil por si só
- Intermediário entre Usuário e Hardware
- Alocador de Recursos (Tempo de CPU, Memória, Arquivos, E/S)
- Programa de Controle


Necessidade
-----------

O objetivo dos sistemas de computação é executar e resolver os problemas do
usuário. Para isto existe o Hardware. O Hardware por si só é particularmente
"difícil de usar". Por isso existem os programas aplicativos, que executam as
funções úteis para o usuário. Todos os programas aplicativos exigem funções de
controle e entrada e saída comuns. Todas estas funções comuns são então reunidas
num único software: o Sistema Operacional.


Como é um sistema operacional?
------------------------------

Esta definição pode variar tanto quanto os tipos de sistemas operacionais
existentes:
Há sistemas que necessitam de menos de 1 MB de memória e não possuem sequer um
editor de tela cheia, enquanto outros ocupam centenas de MB e tem uma interface
gráfica avançada com janelas.
Uma definição mais comum é a de que o sistema operacional é um programa (kernel
ou núcleo) que fica o tempo todo sendo executado e todo o resto são aplicativos.
- Citar caso de Departamento de Justiça X Microsoft e Internet Explorer

Exemplos:
- Características e comparação dos sistemas operacionais:
- DOS: Linha de comando, ocupa pouco espaço, executa um programa por vez
(monotarefa)
- Windows/MacOS: Interface gráfica, ocupam muito espaço, executam diversos
programas (multitarefa)
- Linux e Unix em geral: Linha de comando com Interface gráfica sendo um
aplicativo, ocupa relativamente pouco espaço, multitarefa e multi-usuário, +
eficiência e - conveniência


Conveniência X Eficiência
-------------------------

Conveniência: Facilidade de uso -> Computadores Pessoais / Windows, MacOS

Eficiência: Uso eficiente de computadores caros, compartilhados e de grande
porte -> Sistemas Multiusuário / Unix, OS/2, VMS


Conceitos básicos
=================

**Processo:** Um programa em execução. Precisa de recursos (CPU, Memória, Arquivos,
Dispositivos) para realizar uma tarefa. Unidade de trabalho. Execução
simultânea. Função do SO: Controlar criação, exclusão, escalonamento, mecanismos
de sincronização, comunicação e tratamento de deadlocks.

**Thread:** Múltiplos fluxos de execução em um mesmo processo, compartilhando
recursos inclusive.

**Deadlock:** Vários processos concorrem pelos mesmos recursos, sendo que um está
travando o do outro.

**Memória:** Todos os programas para serem executados devem estar (ao menos
parcialmente) na memória principal e o SO deve coordenar isso.

**Memória virtual:** Utilização de disco para se obter a ilusão de mais memória
principal disponível.

**Sistema de arquivos:** Arquivos em si, sistema de diretórios, proteção.

**Entrada e saída:** O sistema de E/S é dividido em 2 partes:
- Subsistema de E/S (I/O): trata dos aspectos gerais a todos os dispositivos.
- Módulos de driver de dispositivo (Device driver modules): trata das
particularidades de cada dispositivo.
- Placa controladora do dispositivo: hardware destinado a controlar o
dispositivo em si.

**Proteção:** Controla acesso a processos, programas e protege "um programa do
outro".

**Segurança:** Impede acesso não-autorizado e consequente alteração/destruição de
dados do sistema.

Questões para estudo
====================

1. Cite as principais funções de um SO.

2. Quando é apropriado sacrificar eficiência em favor da facilidade de uso
(conveniência)? E o contrário (+ eficiência e - conveniência)?

3. Quais sistemas operacionais você conhece/usa em casa e no trabalho?

4. Defina com suas palavras o que é um processo.

5. Por que é importante que o SO disponibilize um acesso uniforme aos diversos
tipos de dispositivos de E/S?

6. O que você classificaria como fazendo parte de um SO? Ele deve incluir
programas de edição de vídeo, acesso à Web, e-mail e comunicação instantânea?
Por quê?

