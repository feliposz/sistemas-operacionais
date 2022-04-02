Sistema de Arquivos
===================

A parte mais visível do Sistema Operacional do ponto de vista dos usuários. É
função do Sistema de Arquivos prover uma abstração dos meios de armazenamento,
numa estrutura lógica de organização dos dados.

Arquivos
========

Um arquivo é uma coleção de informações correlacionadas, identificado por um
nome. É a menor unidade de armazenamento secundário do ponto de vista do
usuário.

Atributos de um arquivo: Nome, tipo, posição no dispositivo de armazenamento,
tamanho, informações de proteção, data e hora de criação/modificação e
identificação do usuário dono do arquivo.

Tais atributos são mantidos na estrutura de diretório.

As operações que o SO disponibiliza para trata dos arquivos são:
- **Criação:** O SO verifica se há espaço disponível no dispositivo de armazenamento
e aloca para o novo arquivo. Depois cria uma entrada no diretório com o nome e
demais informações sobre o arquivo.
- **Escrita/Leitura:** Para escrever em, ou ler de um arquivo, o SO precisa receber
através de uma chamada de sistemas o nome do arquivo e as informações a serem
escritas ou a posição da memória onde as informações lidas devem ser colocadas.
Em ambos os casos o SO deve acompanhar através de um ponteiro a posição do
arquivo onde estão sendo realizadas as operações e atualizar este ponteiro a
cada operação.
- **Reposicionamento:** Posiciona o ponteiro  de escrita/leitura para a próxima
operação.
- **Exclusão:** Pesquisa-se a entrada do arquivo no diretório e todo espaço alocado
àquele arquivo é liberado. Em seguida a própria entrada no diretório é excluída.
- **Truncar um arquivo:** Reajusta o tamanho  do arquivo para zero, mantendo todos os
outros atributos.

Operações adicionais como renomear, copiar, mover e obter informações sobre os
arquivos são baseadas nestas outras operações primitivas.

A maioria destas operações requer uma busca no diretório pelas informações do
arquivo. Para evitar esta busca contante, o SO mantém uma tabela do arquivos
abertos em memória. Duas operações adicionais são necessárias: Abrir e Fechar
(Open e Close).

A chamada de sistema "open" retorna um índice com a entrada na tabela dos
arquivos abertos. Todas as demais operações são feitas com base neste índice,
inclusive para fechar o arquivo.

Algumas operações adicionais são disponibilizadas em ambientes multiusuário,
como bloqueio de partes de um arquivo usado por mais de um processo, mapeamento
em memória (para acesso mais rápido ao arquivo), etc.

Tipos de arquivo
----------------

Alguns sistemas operacionais oferecem suporte a identificação de tipos de
arquivo. Por exemplo, no MS-DOS, os arquivos são identificados por 8 caracteres
que representam o nome, mais 3 representando uma extensão. Quando uma extensão é
EXE, COM ou BAT, o SO trata o arquivo como sendo um programa executável. As
demais extensões são tratadas pelos aplicativos, sendo que o SO não oferece
nenhum outro suporte adicional.

O Unix não fornece um mecanismo "forte" de identificação para os tipos de
arquivo. É possível usar extensões, mas estas não são obrigatórias e geralmente
ficam a cargo do usuário. Alguns tipos de arquivo no Unix são identificados
através de um "número mágico" que é um valor gravado no começo do arquivo.
Dependendo do número pode ser um arquivo executável, um script do usuário ou uma
biblioteca por exemplo.

Estrutura de arquivos
---------------------

Os tipos de arquivo também podem indicar a estrutura interna de um arquivo. No
MS-DOS, arquivos COM e EXE são executáveis, mas possuem uma organização interna
diferente. No Linux (e outros Unix modernos), há dois tipos de executáveis:
"a.out" e "ELF", sendo que ambos também são organizados de forma diferente,
porém o tipo é identificado pelos "números mágicos" citados anteriormente. No
entanto, em ambos os casos a estrutura não foi "imposta" pelo sistema
operacional.

Alguns SOs permitem apenas alguns tipos de estrutura para os arquivos. Embora
facilitem para o programador/usuário o acesso ao arquivo, o tratamento destas
estruturas torna o SO mais complexo e limita o programador a usar apenas as
estruturas providas pelo SO.

Os SOs mais comuns fornecem uma estrutura mínima de organização dos arquivos.
Isto permite flexibilidade máxima, mas pouco suporte. O tratamento dos dados nos
arquivos fica a cargo dos programas.

Métodos de acesso
-----------------

- **Sequencial:** As informações são processadas em ordem, um registro após o outro. É
o método mais comum.
- **Direto:** Os registros podem ser escritos/lidos, em qualquer ordem.
- **Outros:** Outros métodos de acesso podem ser desenvolvidos com base no acesso
direto (usando índices por exemplo).

Diretórios
==========

O diretório é um registro das informações dos arquivos armazenados em um
dispositivo (ou partição).

Operações em diretórios:
- Pesquisar arquivos
- Criar um arquivo (criar a entrada do arquivo no diretório)
- Excluir um arquivo (remover a entrada)
- Listar um diretório
- Renomear arquivo
- Percorrer o sistema de arquivos

Organização de diretórios:

- **Nível único:** Todas as entradas de arquivos estão num único diretório. Cada
arquivo deve ter um nome diferente do outro.
- **Dois níveis:** Cada usuário possui seu próprio diretório. Um mesmo nome de
arquivo pode ser usado por mais de um usuário. Melhor organização do sistema de
arquivos. Todas as operações com arquivos são restritas aos arquivos do usuário
atual. Em alguns sistemas o usuário é proibido de acessar arquivos de outros
diretórios, enquanto em outros pode haver compartilhamento.
- **Árvore:** Em sistemas de arquivo estruturados em árvore, como o do próprio MS-
DOS ou Windows, é possível um número arbitrário de níveis de diretório. O
diretório em si não passa de um tipo especial de arquivo que "aponta" para os
demais arquivos. Cada usuário possui um diretório corrente e as operações com
arquivos são feitas com os arquivos deste diretório. Para mudar de diretório
usa-se uma chamada de sistema apropriada.

    Os arquivos podem ser acessados ainda através de caminhos. No MS-DOS ou Windows,
um caminho absoluto começa com a partição (ou unidade) em que está o arquivo.
Exemplo: C:\TEMP\TESTE.TXT. No Unix ficaria /tmp/teste.txt. Um caminho relativo
começa sempre com base no diretório atual. Supondo que estamos num diretório
"downloads" e queremos acessar um arquivo em
"/tmp/downloads/imagens/desenho.bmp". Pode-se usar um caminho relativo
"imagens/desenho.bmp".

- **Em grafos:** Um sistema em árvores pode ainda ser incrementado com a
possibilidade de se incluir "links" para arquivos ou diretórios que não estão
imediatamente "abaixo" dos diretórios atuais, resultando numa estrutura que mais
se assemelha a um grafo.

    Nos sistemas Unix existem os links simbólicos ou "soft links", que são
referências relativas a arquivos ou diretórios, e os "hard links" que são uma
"cópia" de determinada entrada de diretório. O SO precisa então manter uma
contagem de links, pois quando um arquivo for excluído e houver mais de um link
para ele, apenas o link deve ser apagado e não o arquivo em si. Quando a
contagem de links chegar a 0, aí sim o arquivo pode ser eliminado.

Proteção
========

Tipos de acesso
---------------

Alguns tipos de acesso que podem ser controlados pelo SO: Ler, Escrever,
Executar, Anexar, Excluir, Listar.

No MS-DOS os controles de tipo de acesso são baseados em atributos do arquivo.
Um arquivo tem 3 atributos que controlam acesso: R - Read Only, H - Hidden, S -
System. Arquivos somente para leitura não podem ser gravados. Arquivos
escondidos não podem ser vistos pelo usuário a menos que ele saiba seu nome.
Arquivos de sistema não podem ser excluídos ou movidos.

No Unix há três controles: r - read, w - write, x - execute, que controlam
respectivamente se o arquivo pode ser lido, gravado ou executado. Para
diretórios, significa se é possível listá-los (ls), criar arquivos dentro deles
ou acessá-los (cd).

Listas de acesso
----------------

Em sistemas multi-usuário cada usuário precisa de uma identificação para se
determinar se um arquivo pode ou não ser acessado (e de que forma).

As listas de acesso contém informações para cada arquivo e diretório de quais
tipos de acesso são permitidos a quais usuários ou grupos.

Pode não ser prático manter uma lista de cada usuário que pode acessar um
arquivo e seu tipo de acesso para cada arquivo de sistema, algumas
classificações podem ser usadas. Por exemplo, no Unix, há três classes de
acesso:

- **Proprietário:** O usuário que criou o arquivo:
- **Grupo:** O conjunto de usuários que compartilha aquele arquivo.
- **Outros:** Todos os outros usuários que tem acesso ao sistema.

Este esquema é mais simples e fácil de implementar, mas não é tão flexível
quanto o de lista de acessos.

Estrutura do sistema de arquivos
================================

Organização
-----------

- **Dispositivo e controle de E/S:** É o módulo que controla ao dispositivo físico
de armazenamento.
- **Sistema de arquivos básico:** Só precisa  emitir comandos genéricos aos
dispositivos.
- **Módulo de organização de arquivos:** Conhece os blocos lógicos e físicos usados
por cada arquivo e faz a tradução entre eles, além de prover informações sobre a
alocação do espaço em disco.
- **Sistema de arquivos lógico:** Provê as funções de controle de arquivo, diretório
e proteção visíveis ao usuário e às aplicações. Mantém informações dos arquivos
abertos por quais processos, etc.

Métodos de Alocação
-------------------

- **Alocação contígua:** É preciso saber previamente o tamanho do arquivo a ser criado
e o espaço alocado deve ser contíguo (um bloco após o outro). Tem problemas com
fragmentação. O SO mantém apenas o nome do arquivo, o bloco de início e o número
de blocos usados pelo arquivo. Ideal para o método de acesso direto.
- **Alocação encadeada:** O arquivo é armazenado em blocos (que podem ser dispersos),
sendo que cada bloco possui um "ponteiro" que indica o próximo bloco do arquivo.
O último bloco contém um valor nulo, indicando que chegou ao fim. O SO deve
manter o nome e o bloco de início e o final. Não existe o problema de
fragmentação anterior, mas só pode ser usada efetivamente para acesso
sequencial. No caso de acesso direto, os blocos devem ser lidos em sequência
para chegar ao bloco desejado.

    Este problema pode ser reduzido com o uso de uma tabela de alocação de arquivos
(FAT). Este método é usado no DOS / Windows 9X e OS/2 por exemplo. Ao invés de
colocar as informações de encadeamento em cada bloco, uma tabela é criada no
início do disco em que cada entrada de bloco aponta para a próxima. O problema é
que a cabeça do disco deve constantemente se deslocar para o início do disco
para acessar a FAT.

- **Alocação indexada:** Neste método, cada arquivo passa a ter um bloco de índice
(também chamado de i-node) que aponta para cada bloco alocado pelo arquivo. O
diretório tem o endereço do bloco de índice. Uma forma comum de se usar os blocos
de índices é que eles sejam multiníveis. No Unix, um bloco possui 15 entradas. As
12 primeiras endereçam diretamente os blocos do arquivo. A entrada seguinte é um
bloco indireto simples, que aponta para um segundo bloco que por sua vez aponta
para os blocos do arquivo. A 14a. e a 15a. são respectivamente blocos indiretos
duplos e triplos, o que permite arquivos arbitrariamente grandes (teoricamente
maiores do que o sistema de arquivos em si é capaz de suportar).

Gerência de espaço livre
------------------------

- **Vetor de bits:** O espaço livre pode ser controlado através de um vetor de bits em
que cada bit representa um bloco. É um método bastante eficiente em termos de
desempenho, pois é simples encontrar um bloco livre. Porém, o vetor de bits pode
ficar grande demais para ser contido na memória.
- **Lista encadeada:** Neste método os blocos livres são armazenados em listas
encadeadas. Cada entrada na lista aponta para o início de um espaço vazio e seu
tamanho.

Recuperação
===========

Consistência
------------

Por questões de eficiência, informações de diretório ou de arquivos podem ser
mantidas na memória principal por um tempo antes de serem gravadas em disco.
Atualizações nos arquivos ou diretórios podem não ser gravadas imediatamente no
sistema de arquivos. No caso de uma falha de hardware (ou mesmo queda de
energia, por exemplo) estas informações podem ser perdidas total ou parcialmente
e portanto o sistema de arquivos pode ficar num estado inconsistente. Quando o
sistema é iniciado um programa especial compara as entradas de diretórios com os
blocos de dados procurando eventuais inconsistências e tentando corrigi-las.

Backup e restauração
--------------------

Como os discos magnéticos podem eventualmente falhar ou mesmo dados podem ser
perdidos devido a erros em programas ou alterações mal-intencionadas é preciso
manter uma cópia de segurança atualizada dos dados. O backup é feito
rotineiramente através de programas de sistema. Em caso da perda de algum
arquivo, diretório ou mesmo unidade inteira, seus dados podem ser restaurados da
cópia de segurança.


Questionário
============

1. Quais informações de um arquivo o SO deve manter na entrada de diretório?

2. Qual a diferença entre os métodos de acesso a arquivos sequencial e direto?

3. Num sistema de diretórios em árvore, dê um exemplo de caminho relativo e absoluto.

4. Num sistema Unix, descreva quais acessos são permitidos aos arquivos da seguinte 
listagem, baseado nos tipos de acesso:

~~~
Permissões  Dono   Grupo  Arquivo ou diretório
-----------------------------------------------
drwxrwxrwx  joao   users  documentos/
-rw-r-----  maria  maria  receita.txt
-r-x--x---  jose   users  programa
~~~

Lembrando que r = leitura, w = escrita, x = execução e que o primeiro caractere 
indica se o arquivo é um diretório e os outros dividem se em 3 grupos de 3:
proprietário, grupo e outros usuários.