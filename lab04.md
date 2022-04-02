Ferramentas de processamento de texto
-------------------------------------

Os sistemas Unix são especialmente práticos para processamentos relativamente
complexos de textos sem exigir programação, graças a diversas ferramentas que
estão à disposição do usuário.

`echo` - Simplesmente exibe o que foi passado como parâmetro. Ex: 

~~~sh
echo OLA MUNDO!
~~~

`cat` - Exibe o conteúdo dos arquivos passados como parâmetro. Ex: 

~~~sh
cat texto1
cat t1 t2 t3
~~~

`wc` - Conta o número de linhas, palavras e letras (wc = Word Count)

`less` / `more` - Exibe a saída de um comando página por página (use as setas, ENTER
ou Espaço para rolar o texto e "q" para sair). Ex:

~~~sh
less /etc/inittab
~~~

`head` / `tail` - Mostra as primeiras/últimas linhas de um arquivo. Ex: 

~~~sh
head /etc/passwd
tail 3 /etc/passwd
~~~

`grep` - Faz uma filtragem apenas das linhas que contém uma expressão. Ex: 

~~~sh
grep bash /etc/passwd #mostra apenas as linhas de /etc/passwd que contém a palavra bash).
~~~

`sort` - Ordena as linhas da entrada. Ex: 

~~~sh
sort -n numeros.txt
sort -d dicionario.txt
sort /etc/group
~~~

Redirecionamento
----------------

É possível redirecionar a entrada ou saída de um comando para um arquivo. Os
operadores para redirecionar são:

`>` - Redireciona a saída. Ao invés de ser exibida na tela, a saída será impressa.
`<` - Redireciona a entrada. Ao invés de ser lida do teclado, será lida do arquivo.
`>>` - Acrescenta ao arquivo ao invés de sobrescrevê-lo (o que seria feito com `>`).

Por exemplo: se quiséssemos gerar uma lista com todas as linhas do arquivo
/etc/passwd e /etc/group que contenham a expressão "bin" e ordená-las faríamos:

~~~sh
cat /etc/passwd /etc/group > lista.txt
grep bin < lista.txt > filtrado.txt
sort < filtrado.txt > ordenado.txt
echo PRONTO! >> ordenado.txt
more < ordenado.txt
~~~

Existe ainda um operador especial conhecido como "pipe", cuja função é
transformar a saída de um comando na entrada do outro. As operações acima
poderiam ser feitas com uma única linha de comando:

~~~sh
cat /etc/passwd /etc/group | grep bin | sort | more
~~~

Ao invés de gerar uma série de arquivos temporários os comandos iriam receber
automaticamente a entrada do anterior.

Apesar de parecer complexo a princípio, você irá perceber que estas são
funcionalidades muito práticas e úteis. Se dominá-las completamente em pouco
tempo irá perceber como é possível fazer muitas coisas em sistemas Unix com as
ferramentas já existentes.

Montando sistemas de arquivo manualmente
----------------------------------------

No linux (e em qualquer Unix), para acessar algum dispositivo removível é
preciso "anexá-lo" ao sistema de arquivos. Este procedimento é chamado de
montagem. Um dispositivo é representado no linux como um arquivo especial no
diretório /dev. Os principais são:

- /dev/cdrom - Representa o drive de CD.
- /dev/fd0 - Representa a primeira unidade de disquete (fd1 para a segunda, se
houver). É o drive A: no DOS/Windows. OBS: FD = Floppy Disk
- /dev/hda, hdb, ... - Representa os discos rígidos (ou mesmo drives de CD/DVD)
padrão IDE (os mais comuns).
- /dev/scd0, scd1, ... - Representa os discos padrão SCSI.
- /dev/hda1, hda2, ... - Representa as partições lógicas dos discos rígidos. Em
casos em que se tem o Windows ou DOS instalados na mesma máquina, o Windows
deverá estar na partição /dev/hda1.

Para saber quais dispositivos estão montados atualmente, basta entrar com o
comando "mount". Isto irá exibir os dispositivos montados e em quais diretórios
eles são acessados.

Para usar um dispositivo no linux, usa-se também o comando mount da seguinte
forma:

~~~sh
mount /mnt/floppy # Para montar o drive de disquete.
mount /mnt/cdrom  # Para montar o drive de CD
~~~

IMPORTANTE: Não se deve remover um dispositivo enquanto ele estiver montado,
pois operações pendentes podem ser perdidas.

Para desmontar um dispositivo use o comando umount (OBS: não é unmount e sim
umount):

~~~sh
umount /mnt/floppy
umount /mnt/cdrom 
~~~

(você ainda pode usar `eject /mnt/cdrom`, no lugar de umount, para ejetar o CD)

Pode ser que em algum caso você precise montar um dispositivo de uma forma
específica. Para saber como os dispositivos são montados por padrão, consulte o
arquivo "/etc/fstab".

~~~sh
cat /etc/fstab
~~~

No entanto, é preciso ter privilégios de Administrador para montar os
dispositivos de uma forma que não esteja prevista no /etc/fstab. Consulte a
seção de usuários e privilégios. Para montar um dispositivo de uma maneira
específica, há algumas opções a serem passadas para mount, por exemplo:

~~~sh
mount -t msdos /dev/fd0 /mnt/floppy
~~~

Neste exemplo, monta-se um disquete do dispositivo /dev/fd0 no diretório
/mnt/floppy com um sistema de arquivo do tipo MSDOS. Você pode alterar o
dispositivo para o desejado e mesmo o diretório onde ele será montado. Se o
disquete tiver sido formatado com algum sistema de arquivo diferente do usado
pelo DOS pode-se especificar no parâmetro -t. É possível acessar sua partição do
DOS ou Windows a partir do Linux:

~~~sh
mount -t vfat /dev/hda1 /mnt/win_c
~~~

A primeira partição (/dev/hda1) será montada no diretório /mnt/win_c
(importante: o diretório deve ser previamente criado!) com o sistema de arquivo
FAT16 ou FAT32 (usado pelo DOS e Windows 95/98). Os sistemas de arquivo NTFS
(usado pelo Windows NT/2000/XP) pode ser usado também, mas somente para leitura.

Visualize os arquivos abaixo com "cat":
- /etc/fstab - Sistemas de arquivo que são montados automaticamente pelo linux
- /etc/mtab - Sistemas atualmente montados. Essencialmente a mesma coisa que a
saída do comando mount.

Usuários
--------

O Unix é um sistema operacional Multi-usuário. Diversos usuários podem acessá-lo
simultaneamente e todos devem se identificar ao entrar no sistema (login).
Existe um usuário especial, chamado de "root" que é o administrador do sistema.
Ele tem privilégio para executar operações que os outros usuários não tem por
padrão. Não se deve usar o root para a operação normal do sistema, apenas para
configuração, instalação de programas e outras atividades privilegiadas.
Qualquer erro cometido enquanto se está com privilégio de root pode comprometer
o funcionamento e a segurança do sistema.

Informações de usuário
----------------------

- `id` - Mostra a identificação do usuário no sistema.
- `whoami` - Mostra seu nome de usuário
- `who` - Mostra uma lista dos usuários conectados

Consulte os arquivos /etc/passwd e /etc/group para saber mais sobre os usuários
existentes no seu sistema.

Criação e administração de usuários
-----------------------------------

Para controlar os usuários do sistema é preciso entrar no sistema como usuário
root. Para isso efetue logoff do seu usuário atual e entre no sistema como root.

É possível adicionar um sistema através da linha de comando com o comando
"useradd *nome_usuario*" e depois definir uma senha com o comando "passwd
*nome_usuario*".

O usuário root pode inclusive acessar o sistema como qualquer usuário usando o
comando "su *nome_usuario*". OBS: Se você estiver como um usuário comum pode
inclusive acessar o sistema como root, apenas digitando "su" e a senha em
seguida.

É possível criar um usuário também através da ferramenta linuxconf disponível em
alguns sistemas. Se não houver uma entrada para o linuxconf nos menus, abra um
terminal e digite "linuxconf". Em Configuração/Usuários/Contas de Usuários, você
poderá gerenciar os usuários de forma gráfica, sem precisar recorrer aos
comandos do modo texto.

Após adicionar um usuário de teste, efetue logoff e faça login como este novo
usuário (não esqueça de selecionar o tipo de sessão, no caso KDE). Veja
informações nos exercícios abaixo.

Para facilitar a administração do sistema, pode-se criar grupos de usuários,
sendo possível então que os usuários de um mesmo grupo tenham acesso comum aos
mesmos privilégios, arquivos e programas, facilitando a administração do
sistema.

Permissões e propriedades de arquivos
-------------------------------------

Em sistemas multi-usuário cada arquivo possui um dono. Você pode ver o dono de
um arquivo através do comando "ls -l". Para alterar o dono de um arquivo use o
comando "chown" (Change Owner). Um arquivo pode ser compartilhado por um grupo
de usuários também. Para alterar o grupo a que pertence um arquivo, use "chgrp"
(Change Group). Exemplos:

- `chown aluno aula.txt` - Altera o dono do arquivo "aula.txt" para o usuário
"aluno". Somente o usuário pode alterar o dono de um arquivo livremente.
- `chgrp prog hello.c` - Altera o grupo do arquivo "hello.c" para "prog". Um usuário
só pode mudar o grupo de um arquivo que lhe pertence, para um outro grupo de
qual faça parte.

Permissões
----------

Em sistemas Unix, os arquivos e diretórios tem permissões individuais. Há três
tipos básicos de permissão: Leitura (R=Read), Escrita (W=Write) e Execução (X=
Execute). Por exemplo, se um arquivo tem permissão para leitura, mas não tem
permissão de escrita e execução significa que é possível examinar seu conteúdo
mas não alterá-lo.

Estas permissões são divididas em 3 segmentos: Dono (User), Grupo (Group) e
Outros (Other). As permissões do dono e grupo são referentes ao que os donos do
arquivo pode fazer com ele. Já as permissões de Outros, referem-se ao que os
demais usuários do sistema podem fazer com estes arquivos. As permissões de um
arquivo pode ser verificadas pelo comando "ls -l". Exemplos:

~~~sh
$ ls -l /tmp
-rw-r--r--    1 root     root       4090  Set 18 08:11 teste.txt
-rwxr-x---    1 teste    users      5000  Set 18 08:15 aula
drwxr-xr-x    2 aluno    aluno      1024 Set 19 12:07 lixo
~~~

O primeiro campo da listagem, composto por traços e mais alguns caracteres
indica as permissões de acesso ao arquivo. A primeira coluna em geral indica o
tipo do arquivo (- é um arquivo comum, d é um diretório e outros caracteres
indicam um arquivo especial, como um dispositivo). As outras colunas são
divididas em 3 grupos:

    u   g   o
    --- --- ---
    rwx rwx rwx

    u - Permissões de dono
    g - Permissões de grupo
    o - Permissões de outros usuários

    r - leitura
    w - escrita
    x - execução

O arquivo teste.txt acima pode ser lido e escrito por seu dono "root" e somente
lido pelos usuários do grupo root e demais usuários. O arquivo "aula" é um
programa que pode ser lido, modificado ou executado por teste. Ele pode ser lido
e executado pelos outros usuários do grupo users, mas não pode ser modificado.
Ele não pode ser acessado pelos outros usuários.

As permissões de diretório são um pouco diferentes. "r" indica se os arquivos do
diretório podem ser listados. "w" se o usuário tem permissão de criar e alterar
arquivos naquele diretório. "x" se é possível acessar (com o comando cd) o
diretório.

Para alterar as permissões de um arquivo usa-se o comando "chmod".

Exemplos:

~~~sh
chmod u=rw,g=r,o= texto_aula
~~~

Faz com que o arquivo "texto_aula" possa ser lido e alterado pelo próprio dono e
somente lido pelos usuários do grupo. Os outros usuários não podem acessar o
arquivo.

~~~sh
chmod +x programa
~~~

Faz com que o arquivo "programa" possa ser executado por qualquer usuário

~~~sh
chmod o-w *.txt
~~~

Remove o privilégio de escrita dos outros usuários de todos os arquivos que
terminam ".txt", sem alterar os privilégios do dono ou grupo.


Exercícios
----------

OBS: Certas operações abaixo exigem que você esteja usando o sistema como
usuário root. Para algumas é suficiente utilizar o comando "su" a partir de um
terminal, enquanto em outros casos é preciso sair e efetuar login como root.
(Consulte o professor para obter a senha.)

1. Use algumas das ferramentas de processamento de texto. Use os comandos more,
less, tail e head para ler os conteúdos de alguns arquivos. O diretório "/var"
contém uma série de logs e históricos do sistema que podem ser consultados.
Redirecione a saída do comando dmesg para um arquivo: "dmesg > dmesg.txt" e use
os comandos "wc", "grep" e "sort" para examinar o arquivo criado.

2. Faça experiências com montagem de dispositivos removíveis. Se tiver um
disquete ou CD em mãos, use o comando "mount" para acessar os arquivos da
unidade. Experimente montar a partição do Windows também conforme explicado
acima. OBS: Não esqueça de criar um diretório "win_c" dentro do diretório
"/mnt".

3. Use os comandos "id", "whoami" e "who" para obter informações da sua sessão
atual. Use o comando "su" em algum terminal e faça login através do console
(CTRL+ALT+F2). Para voltar ao modo gráfico use CTRL+ALT+F7.

4. Crie um usuário chamado "teste" com a senha "0123456". Você pode criar o
usuário através do "linuxconf" ou da linha de comando, como preferir. Saia do
usuário root e efetue login como o usuário teste, recém criado. Altere a senha
para "6543210".

5. Crie alguns arquivos de texto (use o cat ou mesmo um editor gráfico como o
kedit) no diretório "tmp". Usando o root, altere o dono, o grupo e as permissões
de alguns destes arquivos. Experimente acessar posteriormente estes arquivos com
usuários diferentes (use o comando su para alternar entre os usuários) para
verificar os modos de permissão.
