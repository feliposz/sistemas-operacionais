Gerenciamento de processos no linux
===================================

Gerenciando processos no KDE
----------------------------

A forma mais simples de observar os processos sendo executados no linux é com o
gerenciador de processos do KDE. Pressione CTRL+ESC para abrir o gerenciador de
processos e observar os processos em execução. As operações são intuitivas
dispensando maiores explicações. Abaixo veremos os principais comandos para
gerenciar processos no linux através de um terminal.


Comandos para listar processos e jobs
-------------------------------------

`ps` - Lista os processos ativos.

Exemplo:

~~~sh
    ps      # Lista os processos da sessão atual
    ps l    # Lista detalhada dos processos
    ps aux  # Lista processos de todos os usuários (a), fornecendo nome do usuário e quando o processo foi iniciado (u), mostrando inclusive processos não associados a um terminal (x).
~~~

Descrição dos campos:

- PID - Identificação do processo.
- PPID - Parent PID. Identificação do processo pai na árvore de processos
- UID - User ID. Identificação do usuário que criou o processo.
- TTY - Terminal onde o processo está sendo executado.
- TIME - Tempo de processamento consumido pelo processo.
- CMD - Comando referente ao processo
- COMMAND - Linha de comando usada para executar o processo
- STAT - Estado do processo (R - Executando, S - Em espera, T - Parado, etc.)
- %CPU, %MEM, VSZ, RSS - CPU e memória usados pelo processo.

Para mais detalhes consulte a página do manual do ps (man ps).


`jobs` - Lista os jobs (processos sendo executados em segundo plano).

Para colocar um processo em segundo plano pressione CTRL+Z enquanto o processo
estiver sendo executado. Exemplo:

- Entre com o comando: yes > /dev/null
- Pressione CTRL+Z
- Observe a mensagem: [1]+ Stopped   yes  > /dev/null

OBS: O comando yes gera repetidamente a string "y" como saída. Estamos
redirecionando sua saída para /dev/null (um dispositivo especial do linux) para
que não seja impresso nada na tela. Se você esquecer do sinal > pressione CTRL+C
para fechar o processo.

Use o comando "jobs" para ver o processo em segundo plano agora. Repare que ele
está parado (Stopped). Para colocá-lo em execução no segundo plano use o comando
"bg".


Controlando jobs
----------------

bg/fg - Alterna os processos entre primeiro e segundo plano. Para colocar um
processo em segundo plano use "bg *PID*" ou "bg %*JOB*". Exemplo:

Supondo que a saída do comando ps seja:

    PID TTY       TIME CMD
    100 pts/0 00:00:00 bash
    105 pts/0 00:00:00 yes
    120 pts/0 00:00:00 ps

E do comando jobs seja:

    [1]+ Stopped   yes > /dev/null

Você pode colocar o processo em segundo plano usando o comando "bg 105" (usando
o PID) ou "bg %1" (usando o número do Job).

Para colocar o processo em primeiro plano novamente use "fg *PID*" ou "fg
%*JOB*". Para colocá-lo novamente em segundo plano use CTRL+Z.

Experimente executar o editor "vi" e colocá-lo em segundo plano. Para voltar
para o editor digite "fg %*NR. DE JOB DO VI*". Exemplo:

- Execute "vi"
- Pressione CTRL+Z (Aparece a mensagem: [[1]+ Stopped   vi)
- Execute algum outro comando (por exemplo: ls)
- Retorne para o vi com o comando: fg %1
- Para fechar o editor "vi", digite ":q!"" e pressione ENTER.

OBS: Este procedimento é muito útil quando se está usando algum programa
interativo e é preciso executar alguma outra operação no shell.


& - É possível iniciar um processo diretamente em segundo plano acrescentando-se
um & ao final da linha de comando. Exemplo:

~~~sh
yes > /dev/null &
~~~

OBS: Se você esquecer de usar "> /dev/null" o processo estará em segundo plano,
mas imprimindo dados para a tela. Não será possível interrompê-lo com CTRL+C.
Para fazer isto você deve primeiro colocar o processo em primeiro plano . Digite
"fg *ENTER*", mesmo sem ver o que está digitando e depois pressione CTRL+C.


Terminando processos
--------------------

kill - Usado para interromper um processo. Uso: "kill *PID*" ou "kill %*JOB*"
Exemplos:

~~~sh
kill 105
~~~

ou

~~~sh
kill %1
~~~

Normalmente o comando kill envia um aviso ao processo (sinal TERM) para que este
tenha tempo de fechar seus arquivos e terminar normalmente suas operações. Para
forçar o término imediato de um processo (podendo resultar em perdas de
informações, etc) use "kill -s KILL *PID*".

Para interromper o processo sendo executado no momento pressione CTRL+C.

OBS: Somente o usuário "root" pode fechar os processos de outros usuários.


`killall` - Termina um processo através do nome.

Exemplo:

~~~sh
killall yes - Termina TODOS os processos com o comando "yes".
~~~

Controlando prioridades
-----------------------

nice - É possível executar comandos com prioridade diferenciadas. Por exemplo:
Se você precisa ordenar um arquivo ou compilar um programa muito grande e esta
operação será demorada, você pode reduzir o impacto na execução associando
prioridades mais baixas a este processo. Basta executar o processo com o comando
nice:

~~~sh
nice yes > /dev/null &
~~~

A prioridade padrão é 10 (quanto maior o número, mais baixa a prioridade). Você
pode alterá-la com:

~~~sh
nice -n 5 yes > /dev/null &
~~~

OBS: Somente o root pode atribuir prioridades negativas (altas) a um processo.


`renice` - Altera a prioridade de um processo em execução.
Exemplo:

~~~sh
renice 7 177 # Altera para 7 a prioridade do processo de PID 177.
~~~

OBS: Somente o usuário root pode dar mais prioridade para um processo. Os
usuários normais só podem reduzir a prioridade. (Lembre-se que na verdade,
quando maior o valor de nice, menor a prioridade.)


Mais sobre processos
--------------------

`nohup` - Normalmente um processo é terminado quando o processo pai termina.
Portanto, todos os processos iniciados durante uma sessão serão terminados
quando ela for fechada. O comando nohup, faz com que um processo permaneça em
execução mesmo quando o shell for fechado e o usuário tenha efetuado logoff do
sistema. Exemplo:

~~~sh
nohup yes > /dev/null &
~~~

`top` - O programa top permite ver de uma maneira gráfica os processos sendo
executados, sendo que ele atualiza a lista de processos com uma frequência de 1
segundo (pode ser ajustada). Pressione "h" para obter uma ajuda das funções das
teclas no programa.


`/proc` - O diretório "/proc" possui informações sobre processos em execução. Na
verdade ele não foi projetado para ser usado por um usuário e sim por outros
programas que fazem uso destas informações (o programa "ps" consulta os dados de
/proc para exibir informações dos processos). Cada diretório em /proc
representado por números corresponde a um PID de processo. Há outras informações
no diretório /proc referentes à hardware, rede e sistemas de arquivos também.
Repare no entanto, que "/proc" não é um diretório real. Seus arquivos não estão
armazenados em disco algum. Ele é apenas uma representação de informações do
kernel usada por outros programas.


`su` - Além de permitir alternar entre um usuário e outro, o comando su ainda
serve para rodar processos como um usuário diferente. Exemplo:

~~~sh
su aluno -c ls
~~~

ou

~~~sh
su root -c mount -t msdos /dev/fd0 /mnt/floppy
~~~


Exercícios
----------

1. Siga os exemplos apresentados no texto e faça experiências com seus próprios
processos usando os comandos: ps, jobs, fg, bg, top, kill, nice, renice

2. Faça login em um terminal como root e em outro como usuário aluno. Crie um
processo em segundo plano (pode usar o exemplo de "yes" acima) e tente alterar
as prioridades dos processos um do outro (aluno tenta alterar de root e vice-
versa).

3. Crie um processo com o comando "nice cat /dev/random > /dev/null &" e procure
informações sobre ele no diretório /proc/*PID*. É claro, para saber o PID
correto você deve usar o comando ps.

