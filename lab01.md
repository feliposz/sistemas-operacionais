# Laboratório 1: Utilização do modo gráfico do Linux (X Window System)

## 1) Como iniciar o sistema no Linux (tela de seleção de boot) e efetuar o login e logout do sistema.

No tela de seleção de boot (boot loader), que pode ser o XOSL, o LILO ou o GRUB
(estudaremos em detalhes isto depois), selecione Linux (ELX ou Conectiva,
dependendo do caso). Uma série de mensagens irá aparecer (detecção de hardware,
inicialização de serviços, etc) e finalmente uma tela de login deve ser
mostrada.

Entre com o usuário e senha fornecidos pelo
professor. Em tipo da sessão, selecione KDE (um dos gerenciadores de janela do
Linux).

Para sair, clique no ícone na barra inferior, à esquerda (deve estar escrito,
start, início, ou ter o desenho de um K ou uma engrenagem, pode variar bastante
de uma configuração pra outra) e selecione Terminar/Desligar/Shutdown. Escolha
então Logout (ou Login as another user - Login como um usuário diferente).

Se quiser desligar o computador ou reiniciá-lo, escolha desligar/shutdown ou
reiniciar/restart.

## 2) Utilização básica do KDE

### Abrir e fechar aplicativos principais (calculadora, processador de textos, planilha, editores de imagens, jogos, browser)

Para executar um aplicativo, basta clicar sobre o Menu do KDE (que é o ícone que
está na barra inferior à esquerda, na maioria dos casos) e selecionar o programa
que se quer abrir.

Também é possível executar um programa digitando-se seu nome, se você o souber.
Experimente ir em KDE/Run Command ou Executar Comando. Digite "kate" e mande
executar. A janela do editor de textos Kate deverá ser exibida. Se quiser use o
atalho ALT+F2.

Experimente abrir alguns aplicativos, como a calculadora, um editor de textos,
etc.

### Redimensionamento de janelas/Botões principais

Trabalhar com as janelas no KDE (ou mesmo no gnome) é muito semelhante ao
Windows. Os mesmos botões minimizar, maximizar e fechar estão lá (com um desenho
diferente dependendo do caso). Redimensionar e mover também é feito da mesma
forma, arrastando as bordas e a barra de título respectivamente. É possível
"enrolar" as janelas, de forma que só a barra de título fique visível. Basta dar
um duplo clique sobre a mesma. No lado esquerdo da barra de título de cada
janela tem um ícone semelhante ao do Windows, que possui todas estas funções
(minimizar, maximizar, restaurar, fechar, sempre no topo, "shade", etc). Você
pode fechar um programa pressionando ALT+F4.

OBS: Dependendo de como está configurado o KDE, a janela "focalizada" é sempre a
que está sob o mouse ou é preciso clicar sobre ela. Experimente abrir duas ou
mais janelas e mover o mouse sobre elas sem clicar. Verifique se a cor da barras
de título dos programas muda conforme você move o ponteiro do mouse.

O ALT+TAB funciona também no KDE para alternar entre os programas.

### Obtendo ajuda

A ajuda do KDE está disponível em KDE/Help. Se estiver procurando por um tópico
específico pode usar ALT+F2 e no lugar de um comando, digite help:*tópico*. Por
exemplo: "help:konqueror", vai abrir o manual de utilização do browser do KDE, o
Konqueror.

### Customização da área de trabalho (temas,, papel de parede, protetor de tela)

É possível alterar uma série de configurações da área de trabalho (e de outras
coisas também) do KDE através do KDE Control Center. Vá em
KDE/Configuration/Control Center/Look & Feel. Se não achar o ícone no menu do
KDE, ele pode estar na barra inferior ou você pode executá-lo com ALT+F2 e
digitar "kcontrol".

### Virtual Desktops

O X Window System oferece uma funcionalidade de desktops ou áreas de trabalho
virtuais. Você pode distribuir as aplicações que está usando entre os diversos
desktops virtuais.

Você configura os virtual desktops no próprio KDE Control Center em Look &
Feel/Desktops/Number of Desktops.

Para alternar entre os desktops use CTRL+TAB ou CTRL+F1, CTRL-F2, etc. Você pode
"jogar" um aplicativo para ser exibido em outro desktop, clicando-se no ícone do
lado esquerdo da barra de títulos e em "To Desktop". Em seguida escolha para
qual área de trabalho deseja enviá-lo.

O ícone de um alfinete do lado do ícone do aplicativo, quando clicado, faz com
que a janela fique visível em todos os desktops.

## 3) Configurando o proxy dos browsers:

Para acessar a Internet, usando um dos browsers do Linux, será preciso
configurar um servidor Proxy (por estarmos acessando a internet de dentro do
IMAPES, isto não é necessário ao acessar de casa por exemplo).

Abra um dos browser que você preferir, encontre a configuração do proxy (ver
abaixo) e entre com as seguintes informações para os protocolos HTTP, HTTPS, SSL
e FTP.

    Endereço do proxy: xxx.xxx.xxx.xxx
    Porta: 3128

Browsers:
- Konqueror: Settings/Configure Konqueror/Proxies & Cache/Use proxy (V)
- Mozilla & Netscape: Edit/Preferences/Advanced/Proxies/Manual proxy
configuration
- Opera: File/Preferences/Network/Proxy servers
- Galeon: Settings/Preferences/Advanced/Network

## 4) Criar, abrir e editar documentos usando o editor Kate / KNotepad

Abra um editor de textos qualquer (pode ser o "kate" mesmo, que foi explicado
anteriormente. Você vai perceber que ele não é muito diferente de qualquer
programa comum para Windows. Experimente digitar algum texto nele, abrir e
salvar arquivos, etc.

OBS: Ainda não chegamos a trabalhar com arquivos e diretórios, mas procure
salvar sempre seus arquivos na sua própria pasta (geralmente /home/imapes ou
/home/aluno), mesmo porque você não terá permissão do SO para gravar em outras
pastas.

OBS2: Se não gostar da fonte usada pelo "kate" ou se ela estiver muito pequena,
vá em Settings/Configure kate/Editor/Fonts.

## 5) Usando uma janela de terminal

No linux existe uma espécie de prompt de comando (como o prompt de comando do
MS-DOS). A localização do atalho para o Console ou Terminal do linux pode estar
em diversos lugares. Se não estiver já na barra de tarefas, procure por
Terminal, XTerm ou Konsole no menu do KDE. Se ainda assim não encontrar, abra
com ALT+F2 e digite konsole ou xterm.

Para experimentar um pouco com os comandos do prompt do linux, digite alguns
comandos como:

- clear - limpa a tela
- ls - lista os arquivos do diretório atual
- cat *nome do arquivo* - exibe o conteúdo de um arquivo (ex: cat /proc/version)
- less *nome do arquivo* - mostra um arquivo grande e permite "rolar" usando as
setas (ESC para sair)
- pwd - mostra o diretório atual (repare que o linux usa / ao contrário de \ do
windows)
- cd / - vai para o diretório raiz (digite ls novamente para listar os arquivos do
diretório raiz)
- cd *nome do diretório* - entra em um diretório (são as entradas em azul,
listadas pelo "ls")
- cd .. - volta um nível de diretório

Para sair do modo console, digite "exit" ou pressione CTRL+D.

## 6) Entrando e saindo do modo console (texto) e reiniciando o X Server (para casos extremos).

Para entrar no modo console (texto) do linux, pressione CTRL+ALT+F2. Você será
apresentado a uma tela de login e precisará digitar usuário e senha (os mesmos
que para entrar no X Window). Experimente alguns dos comandos que já usou no
terminal no item 5 acima.

Para retornar ao modo gráfico (X Window) pressione CTRL+ALT+F7.

Se em algum caso extremo o X Window ou KDE ficar instável, parar de responder,
etc. Pressione CTRL+ALT+BACKSPACE (<-).

## 7) Arquivos

O "equivalente" do Windows Explorer no KDE é o Konqueror. Com ele é possível
trabalhar com os arquivos e diretórios do sistema de arquivos do Linux de forma
visual. Sua utilização é semelhante à do Windows Explorer. Se quiser ver a
estrutura de diretórios completa do linux digite "/" na barra Location ou clique
no ícone "Root Directory" na guia que exibe as pastas do lado esquerdo. A função
de cada diretório e de alguns arquivos especiais será estudada adiante. Se
quiser ver algum arquivo, clique com o botão direito (como faria com o Windows)
e em Open With (abrir com). Depois selecione o programa que quer usar para ver o
arquivo (ou digite kate, se quiser ver no editor de texto que já conhecemos).

