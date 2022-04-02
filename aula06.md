Gerência de Memória
===================

Os programas e dados precisam estar na memória principal para serem processados
pela CPU. As instruções dos programas são lidas da memória e executadas pela
CPU. Os dados são lidos e gravados por estas instruções. O acesso à memória é
feito através de endereços.

Os programas normalmente são armazenados em disco na forma de código executável
e quando são carregados para a memória devem ter seus endereços ajustados de
acordo com a posição onde serão carregados. Isto chama-se relocação.

A unidade de controle de memória (MMU) é um dispositivo de hardware que faz o
mapeamento dos endereços lógicos para os endereços físicos, baseando-se num
registrador de relocação.

Ligação dinâmica Vs. estática
-----------------------------

Os programas de usuário são ligados às bibliotecas de linguagem do sistema.
Alguns sistemas só permitem ligação estática, isto é, as referências às rotinas
da biblioteca são feitas quando o programa é criado. Com ligação dinâmica, as
referências são feitas quando o programa é carregado na memória para execução. A
vantagem é que o código da biblioteca - que é usado por vários programas - não
precisa ser copiado para cada programa. As bibliotecas usadas por mais de um
programa podem ser compartilhadas, economizando memória e espaço em disco.

Swapping
--------

Um processo precisa estar na memória principal para ser executado. No entanto,
ele pode ser movido para um armazenamento auxiliar (disco) enquanto não estiver
sendo executado e ser carregado posteriormente para continuar a execução. Isto é
chamado de swapping. O swapping é extremamente "caro" pois a troca de contexto é
extremamente lenta, pois para alternar entre processos é necessário gravar e ler
os dados em disco constantemente. O sistema de troca puro, portanto não é muito
utilizado.

Versões modificadas no entanto, podem ser encontradas em sistemas Unix. O
swapping fica desativado enquanto houver espaço disponível na memória principal.
Quando mais processos forem carregados e a memória estiver cheia, processos
inativos ou antigos são descarregados para o disco até haver espaço disponível e
carregados posteriormente.

Alocação contígua de memória
----------------------------

Neste esquema vários processos podem ser carregados simultaneamente em espaços
de memória variável. Seu espaço é delimitado por um registrador de relocação (ou
base) e um de limite (indicando o endereço de memória lógico máximo do
processo). A alocação pode ser feita de acordo com um dos algoritmos:

- **First-fit:** O primeiro espaço livre suficiente para o processo é alocado.
- **Best-fit:** O menor espaço livre suficiente é alocado. Pode resultar em diversos
espaços pequenos fragmentados na memória.
- **Worst-fit:** O maior espaço é alocado, deixando fragmentos maiores que podem ser
mais úteis do que os pequenos fragmentos do best-fit.

Paginação
---------

A paginação reduz o problema de fragmentação, pois não requer que as páginas de
um processo sejam contíguas na memória. O espaço de endereçamento lógico de um
processo é dividido em diversas páginas de tamanho fixo que são mapeadas na memória
física. O endereçamento passa a ser feito através de uma combinação de número de
página mais deslocamento dentro da página. O SO traduz o número da página para o
endereço físico na memória principal.

Segmentação
-----------

No esquema de segmentação, os programas de usuário são divididos em segmentos,
que podem ter tamanho variável. Um segmento pode contar o código principal,
enquanto outro possui dados, outro a pilha, sub-rotinas, etc.

Os segmentos de código podem ser protegidos para somente-leitura ou somente-execução, evitando erros de programação comuns que podem causar problemas
difíceis de detectar. Como o segmento de código pode ser protegido contra
gravação, ele pode inclusive ser compartilhado por outras instâncias do mesmo
programa.

A desvantagem da segmentação é que ela causa fragmentação da memória, assim como
na alocação contígua.

Segmentação com paginação
-------------------------

Tanto a segmentação como a paginação tem vantagens e desvantagens. Os sistemas
modernos tendem a combinar ambas as técnicas para tirar proveito dos pontos
positivos das duas. Neste esquema, cada segmento é por sua vez dividido em
páginas, como no sistema de paginação, evitando a fragmentação da memória.

Memória Virtual
===============

A vantagem da técnica de memória virtual, é que os processos não precisam estar
totalmente carregados na memória para serem executados e ainda podem ser maiores
do que a memória física. Isto libera os programadores das preocupações de
limitação de memória.

Paginação sob demanda
---------------------

O método mais comum de implementação da memória virtual é a paginação sob
demanda. É uma espécie de paginação com swapping, mas neste caso o paginador
(pager) e não "swapper" só carrega para a memória principal as páginas que
realmente serão usadas. O swapper manipula processos inteiros.

Apenas as páginas essenciais de um processo são carregadas para a memória
inicialmente. Uma tabela controla quais páginas estão na memória e quais estão
em disco. Se uma página não está carregada e um processo tenta acessá-la, uma
exceção (page-fault) ocorre e o SO deve tratá-la. O SO interrompe o processo e
carrega a página solicitada. O controle é então devolvido ao processo que pode
acessar a página como se nada tivesse acontecido.

Como só as páginas necessárias são carregadas, mais memória física fica livre e
mais programas podem ser executados simultaneamente.

Substituição de página
----------------------

Conforme o nível de multiprogramação aumenta e mais processos são carregados,
eventualmente, toda memória poderá ser ocupada não sobrando páginas livres. Mas
os processos em execução podem precisar de mais páginas para execução. A solução
é fazer a substituição de páginas.

Se nenhum quadro da memória estiver livre, procura-se um que não esteja sendo
usado no momento e ele é gravado no espaço de swap e liberado na tabela de
páginas. Este quadro passa a estar livre para ser usado.

Há vários algoritmos de substituição:

- **FIFO (*first-in, first-out*):** A página mais antiga a entrar é a primeira a ser liberada.
- **LRU (*least recently used*):** A página menos usada recentemente é liberada.
- **LFU (*least frequently used*):** A página que tiver sido menos usada.

Questões para estudo
--------------------

1. Qual a função do registrador de relocação da unidade de controle de memória
(MMU)?

2. Qual a vantagem da ligação dinâmica para a ligação estática?

3. Num sistema de swapping comum, é possível rodar programas maiores do que a
memória principal?

4. Qual é a vantagem da paginação em relação à alocação contígua?

5. O que é memória virtual?

6. Na paginação sob demanda, como (e quando) são carregadas as páginas para a
memória principal?

