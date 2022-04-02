Instalação do Linux
===================

Introdução
----------

Instalar o Linux não é mais complicado do que instalar qualquer outro sistema
operacional. O problema é que na maioria dos casos as pessoas já compram o
computador com o sistema instalado e em geral pedem para um técnico reinstalar
quando precisam. Isto nem seria necessário, pois o procedimento não é difícil
desde que se tome alguns cuidados.

O fator que complica um pouco a vida de quem vai instalar o Linux é o fato de já
existir um sistema operacional instalado no computador (o Windows em 99% dos
casos) e o usuário não quer ter de reinstalar todo o sistema. Portanto alguns
passos a mais são necessários nestes casos. De início pode parecer complicado e
perigoso, mas não é, desde que sejam observados alguns detalhes.

Em primeiro lugar: É IMPORTANTE FAZER UMA CÓPIA DE SEGURANÇA DE TODOS OS
DADOS!!! Se possível até dos programas, pois em caso de problemas será fácil
recuperar o sistema perdido. Tenha pelo menos um CD de instalação com os
principais programas e drivers que você usa para poder recuperar o sistema se
tudo mais falhar. Veja mais sobre como fazer essa cópia de segurança mais
abaixo.

A instalação do Linux costuma ser tão ou mais rápida que a de outros sistemas
(em geral menos de 20 min, mas podendo levar até uma hora em computadores muito
lentos), mas mesmo assim é bom reservar um bom tempo para o caso de ter
problemas. Uma manhã, tarde ou noite inteira pelo menos. Você não vai querer
complicar sua agenda ou se atrasar para algum evento por causa da mera
instalação de um SO.

AVISO 1: SE VOCÊ NUNCA INSTALOU UM SISTEMA OPERACIONAL ANTES ou já instalou mas
não compreendeu bem as instruções descritas aqui, não tente instalar o Linux ou
outro sistema sozinho, sem o apoio de alguém com mais experiência. Em geral, as
pessoas que usam o linux estão sempre dispostas a ajudar os iniciantes. Não
tenha vergonha e peça ajuda. É melhor fazer isto antes de instalar, do que
depois que já tiver perdido seus dados e não conseguir mais usar seu computador
por conta de algum erro cometido na instalação.

AVISO 2: NÃO ME RESPONSABILIZO PELO USO INCORRETO DAS INSTRUÇÕES APRESENTADAS
AQUI. Instalar um sistema operacional, particionar e formatar um disco rígido
são atividades de risco que podem resultar na perda irreversível de informações
do seu computador, se feitas de forma inadequada. Faça sempre uma cópia dos
dados mais importantes e peça ajuda de alguém que entenda se não estiver seguro
ou não quiser correr riscos.

Obtendo informações do seu sistema
----------------------------------

Os linux atuais tem um excelente sistema de detecção de hardware capaz de
configurar automaticamente a maioria dos dispositivos, sem maiores complicações.
No entanto, algumas placas ou dispositivos podem ser mais complicados de
instalar. Recomenda-se fazer um levantamento de todos os dispositivos instalados
no seu sistema. As chances são que se o dispositivo é detectado normalmente no
Windows, sem necessidade de nenhuma configuração manual, há 95% de chance dele
funcionar no linux (exceto alguns dispositivos mais antigos ou muito novos, e
alguns mais exóticos).

No Windows clique com o botão direito em Meu Computador/Propriedades e vá em
Gerenciador de dispositivos, anote as informações de fabricante (marca) e modelo
dos dispositivos mais importantes (Adaptador de Rede, Modem, Vídeo, CD, Disco
rígido, Som, Monitor, Mouse, Portas, Teclado, Unidades de disco e Controladores
USB, SCSI e PCMCIA). Saiba também o fabricante e modelo da impressora e scanner
e o tipo de conexão (porta paralela, serial ou USB). Isto é tudo para os
dispositivos "Plug & Play". Se você tiver algum dispositivo que não seja padrão
Plug & Play (um modem, placa de som ou rede mais antigos, por exemplo) precisará
anotar informações de interrupção (IRQ), intervalo de memória, DMA e E/S (I/O).
Neste caso, veja as propriedades dos dispositivos e clique em "Recursos" para
anotar as informações deles.

Se seu computador está ligado em rede, procure informações com o administrador
da rede se seu computador possui IP fixo ou dinâmico, qual o nome do domínio e
da máquina local, se o IP for fixo, qual é o IP, máscara de rede, gateway
padrão, DNS, etc.

Ter todas estas informações disponíveis, embora seja desnecessário em alguns
casos, pode lhe poupar muito tempo durante a instalação.

Preparando um disquete de emergência para o Windows
---------------------------------------------------

Requisitos: Você precisará de dois disquetes em branco (vazios) para criar o
disco de emergência do Windows/DOS. Você perderá todos os dados que estão neles
se os discos não estiverem vazios.

1. Abra o Windows Explorer, clique com o botão direito em Disquete de 3 1/2"
(A:) e depois em Formatar...

2. Selecione Tipo de Formatação: Completa e marque a caixa Copiar os arquivos de
sistemas. Este disquete poderá ser usada para dar boot (inicializar o
computador) em caso de algum problema.

3. Copie os arquivos listados abaixo, da pasta C:\Windows\Command
(C:\Windows\System ou C:\Windows\System\Command dependendo do caso) para o
disquete. Eles são essenciais:

    Edit.com - Um editor de texto simples
    Fdisk.exe - Ferramenta para visualizar e editar as partições do disco rígido
    Format.com - Usado para formatação de discos
    Sys.com - Instala a base do sistema operacional (apenas DOS) para um disco

4. Copie também os seguintes arquivos (que estão na mesma pasta) que podem ser
úteis:

    Chkdsk.exe - Faz uma checagem simples no disco
    Scandisk.exe - Faz uma verificação completa no disco
    Himem.sys - Driver de memória estendida, necessário para rodar algumas versões
    do scandisk
    Xcopy.exe e Xcopy32.* - Faz cópias de árvores de diretório inteiras
    Mem.exe - Exibe quanto há de memória RAM disponível

5. Estes arquivos podem ser encontrados também no CD de instalação do Windows.
Você ainda pode criar um disquete semelhante (com mais ferramentas até,
inclusive suporte a CD em alguns casos) indo em: Iniciar/Configurações/Painel de
controle/Adicionar ou remover programas/Disco de inicialização e clique em Criar
disco. Siga as instruções. No entanto, por copiar ferramentas a mais, haverá
possivelmente menos espaço no disquete para outras ferramentas do linux que
vamos copiar depois.

OBS: É recomendável ter um disco de inicialização reserva em caso do primeiro
falhar! Não economize, é melhor fazer dois discos de inicialização.

É possível criar o disquete através do prompt de comando do DOS, com os
seguintes passos:

Formatar o disquete -> 
    
    format a: /s

Copiar os arquivos necessários ->

     copy c:\windows\command\fdisk.exe a: 
     
(repetir para todos os outros arquivos listados)

6. Se você possui em mãos um CD de instalação do Linux, é muito provável que no
primeiro CD (ou no único se for o caso) exista uma pasta chamada "dosutils" ou
"tools". Copie os seguintes arquivos desta pasta para o disquete:

Fips.exe - Ferramenta que permite fazer um reparticionamento "não-destrutivo" do
disco rígido. Isto é, você pode reparticionar sua atual partição do Windows (que
deve estar ocupando o disco todo) liberando espaço para ser usado pelo Linux.
Restorrb.exe - Esta ferramenta recupera as mudanças feitas pelo fips.exe em caso
de falha no particionamento, para o caso do Windows parar de funcionar.
Rawrite.exe - Copia uma "imagem" de um disquete para um arquivo e vice-versa.
Útil se você precisar criar um disco de boot para o linux.

Se ainda houver espaço copie a pasta fipsdoc ou pelo menos o arquivo fips.doc
(que poderá ser lido com o edit.com copiado acima) para o caso de precisar de
informações especiais sobre o FIPS.

7. Se você copiou o arquivo himem.sys e pretende usar o scandisk para verificar
possíveis erros no disco (recomendado), crie um arquivo chamado "config.sys" no
disquete com o seguinte conteúdo:

    DEVICE=A:\HIMEM.SYS

OBS: Cuidado! O nome do arquivo deve ser exatamente este: CONFIG.SYS. Você deve
criar um arquivo texto "puro". Pode usar o Bloco de Notas para isso ou o próprio
programa Edit.com que copiou para o disquete.

Verificando se o disquete de inicialização funciona
---------------------------------------------------

Reinicie seu computador e deixe o disquete no drive para que a inicialização
seja feita por ele. (Pode ser necessário mudar um parâmetro no Setup da BIOS do
seu computador se não estiver conseguindo iniciar pelo drive.)

Deve aparecer um prompt de comando (A:\>):

- Execute o programa fdisk (digite "fdisk" e tecle *ENTER*) e para ver as
partições existentes do seu disco tecle 4. Saia do programa SEM FAZER ALTERAÇÕES
NO DISCO.

- Execute o fips em modo teste (digite "fips -t" + *ENTER*) para ver como será
feito o reparticionamento do seu disco por ele.

- Execute o programa scandisk no disco em que pretende instalar o linux
(scandisk C:, por exemplo). O scandisk fará uma verificação no seu disco em
busca de erros, poupando muitas dores-de-cabeça. Ele irá perguntar se você quer
fazer um exame de superfície. Este exame pode ser bem demorado dependendo do
tamanho e da velocidade do seu disco rígido, mas é extremamente recomendado se o
seu HD não for lá muito novo e você não fez nenhum exame completo do seu disco
rígido recentemente.

Criando um disquete de inicialização do Linux
---------------------------------------------

Requisito: Um disquete em branco (se possível mais de um para o caso do primeiro
falhar)

Você vai precisar de um disquete de inicialização do Linux se seu computador não
permite boot através do drive de CD ou se pretende instalar via rede ou em
outros casos especiais.

1. Verifique se no CD de instalação do linux que você possui existem os
diretórios "dosutils" e "images". Na pasta dosutils deve haver um programa
rawwritewin.exe ou rawrite.exe que será usado para criar o disco. Verifique
quais imagens estão disponíveis em images. Um arquivo boot.img deve estar
presente, é este que será usado. Podem haver outras imagens para instalação via
rede, ou via internet, mas não trataremos destes casos especiais aqui, consulte
a documentação da distribuição que está usando para mais detalhes.

2. Execute o programa rawwritewin.exe ou rawrite.exe (para DOS) e informe o
drive em que será gravado o disquete e qual arquivo de imagem será usado.

3. Se não ocorreram erros na gravação do disquete ele está pronto. Você pode
testá-lo antes de instalar simplesmente reiniciando a máquina. Se tudo correu
bem, para reiniciar o computador novamente no Windows depois que o disquete de
boot for carregado, basta remover o disquete e pressionar CTRL+ALT+DEL ou
apertar o botão RESET.

OBS: Experimente iniciar o sistema apenas com este disquete. Se ocorrer algum
problema na detecção do hardware pode ser necessário criar a imagem de um
segundo disco de suporte, contendo alguns módulos de drivers de dispositivo
adicionais. Você vai precisar de mais um disquete em branco e use a imagem
chamada "drivers.img" ou "modules.img" dependendo da distribuição que estiver
usando. Se não for nenhum destes, procure informações na documentação do CD, ou
na internet.

Cópia de segurança
------------------

É fundamental ter uma cópia de segurança ou backup dos dados mais importantes do
seu computador. Desculpe se estou sendo repetitivo neste ponto, mas é para
evitar-lhe muitas dores-de-cabeça se alguma coisa der errada. Você não precisa
se preocupar, as chances de problema são pequenas, mas segurança nunca é demais.

Há várias formas de copiar seus dados: disquetes, CDs (se você tiver um
gravador, ou puder pedir emprestado de algum amigo), zip drive (idem), outros
computadores (se estiver em rede), outro disco rígido (se tiver mais de um no
seu computador), outra partição (recomendado apenas para usuários experientes,
que sabem o que estão fazendo), fitas magnéticas (em geral usado nas empresas
para grande volume de dados). Em último caso você pode usar a internet para
copiar para o computador de um amigo (de confiança, é claro) seus dados ou usar
um serviço de "drive virtual". Mas isto é apenas para quantidades pequenas, pois
a cópia pode ser bem demorada.

Aqui vai uma lista pra você se lembrar do que é essencial copiar. Os itens que
vem antes são mais importantes na minha opinião, mas você pode dar prioridades
diferentes no seu caso:

- Documentos e arquivos pessoais (inclusive trabalhos para escola, fotos, etc)
- Arquivos usados no trabalho (documentos, programas, projetos)
- Pastas de arquivos do Windows (Meus Documentos, Meu porta-arquivos, Favoritos,
Arquivos gravados na área de trabalho) caso você as use
- Cópia de informações de contatos e histórico de programas de e-mail e
mensagens instantâneas (ICQ, MSN Messenger, etc.)
- Programas de instalação de drivers atualizados, caso você não tenha os CDs ou
disquetes que acompanham o computador
- Instaladores dos programas mais usados, caso você não tenha os CDs ou
disquetes de instalação
- Arquivos baixados da internet (Downloads)
- Músicas
- Vídeos
- Jogos (você pode optar por copiar só os arquivos de jogos salvos para
economizar espaço, que podem ser recuperados depois de reinstalar o jogo)
- Arquivos com menor importância se sobrar espaço

Se não tiver espaço suficiente para copiar tudo, dê maior importância aos itens
listados primeiro e menor importância aos itens listados depois (mesmo porque
são bem maiores, em especial, músicas, vídeos e jogos). Se tiver espaço de sobra
você pode criar uma "imagem" ou seja, uma cópia exata do disco ou da partição
que tem e gravá-la em outro disco, partição ou mesmo em CDs, usando um programa
apropriado.

Para economizar espaço use um programa de compactação (WinZip, WinRar, WinAce),
mas também certifique-se de que tem o instalador do programa para recuperar os
arquivos.

Particionamento do disco rígido
-------------------------------

CUIDADO! Reparticionar um disco rígido incorretamente pode causar perda
permanente de informações importantes do seu computador! Assegure-se de ter uma
cópia atualizada de todas as informações importantes que possui e os CDs ou
disquetes de instalação de todos os programas instalados, para o caso de uma
falha ocorrer.

A maioria das distribuições modernas de linux permitem o reparticionamento não-
destrutivo do disco rígido usando uma ferramenta gráfica e intuitiva. Se não for
este seu caso, aqui está descrita uma ferramenta gratuita que é recomendada
apenas para os usuários mais experientes. Só use os métodos a seguir se souber
exatamente o que está fazendo, caso contrário recomenda-se o acompanhamento de
alguém mais experiente.

Espaço de particionamento
-------------------------

Dependendo do tamanho do disco rígido, do espaço que você usa no Windows e de
qual distribuição pretende instalar você pode fazer vários modelos de
particionamento diferentes. Se comprou seu computador recentemente as chances
são que você tenha no mínimo 10GB de espaço em disco, embora seja possível "se
virar" com menos.

O tamanho da instalação das distribuições pode variar muito.
A Red Hat 9, uma das mais atuais, pode consumir desde 500MB na instalação mínima
até 5GB na mais completa (logicamente, instalando-se TODOS os pacotes que se tem
direito), sem considerar os dados e programas a serem instalados posteriormente
pelo usuário. Logo, vou considerar os seguintes esquemas de particionamento
recomendados para iniciantes:

Tamanho do HD   | Windows   | Linux
----------------|-----------|-----------
2GB (*)         | 1.2-1.5GB | 500-800MB
6GB             | 4GB       | 2GB
10GB            | 7GB       | 3GB
20GB            | 13-15GB   | 5-7GB
40GB (ou maior) | -         | 10GB (**)

Estou considerando que você vá usar muito mais o Windows do que o Linux e
portanto vai precisar de mais espaço para o primeiro. De qualquer forma, os
programas para o Linux tendem a ser menores e numa partição menor é possível ter
até mais utilitários que no Windows.

(*) É um pouco mais difícil "fazer caber" uma instalação de um linux "normal"
numa partição menor que 1 GB, mas não é impossível. Porém não espere conseguir
fazer muita coisa e instalar muitos pacotes (mesmo o espaço do Windows será
dramaticamente reduzido). Em geral você precisará instalar a configuração mínima
e talvez ainda tenha que tirar alguns pacotes manualmente, sem considerar que
vai precisar criar uma partição de swap (memória virtual). Há distribuições
criadas exclusivamente para serem instaladas em partições menores, procure se
informar a respeito (embora o preço de discos rígidos maiores tenha baixado
bastante ultimamente).

(**) 10GB em geral é mais do que suficiente pra qualquer distribuição para uso
doméstico. Logicamente, em servidores de arquivos ou banco de dados numa
empresa, será necessário muito mais espaço.

Estes valores são meras estimativas, procure ler a documentação da distribuição
que pretende instalar para ter uma idéia melhor de quanto espaço reservar.

Além disso, no linux é necessária uma partição chamada de swap, usada para
memória virtual. Se tiver muita memória disponível em sua máquina (256 ou 512MB)
talvez você nem precise criar uma, mas é sempre uma boa idéia. A memória virtual
usa espaço em disco para simular a existência de mais memória física disponível.
Há vários esquemas de configuração de memória virtual, você pode deixar o
instalador configurar isto ou preferir definir o tamanho manualmente. Não
esqueça que você deve contar com o tamanho da memória virtual também ao
particionar seu disco. Talvez queira reduzir um pouco o tamanho da partição
linux ou windows para isso.

Particionamento destrutivo
--------------------------

Se já pretende reinstalar o Windows é conveniente reparticionar o HD de forma
"destrutiva", isto é: apagar todas as partições existentes e recriá-las. Para
isto, você deve reiniciar o sistema com o disco de inicialização do DOS/Windows
mencionado acima e executar o utilitário de particionamento do DOS, o "fdisk".

Usando o fdisk, apague todas as partições existentes (opção 3) e crie uma
partição primária para o Windows (opção 1) do tipo FAT32 (se for instalar o
Windows 95/98, Me). Se for instalar o Windows 2000 ou XP, eles tem um utilitário
de particionamento próprio e você deve preferir usá-lo. Você pode criar uma
partição do tipo NTFS mas neste caso não poderá acessá-la completamente do Linux
(apenas para leitura, pois o driver ainda é experimental). Partições FAT32 podem
ser acessadas sem problemas do Linux.

Ao definir o tamanho da partição coloque o tamanho que decidiu (veja sessão
anterior) e pronto. Depois disto basta formatar a nova partição (FORMAT C: /S ->
para formatar e copiar os arquivos de sistema). Você já pode até reiniciar seu
computador diretamente do disco rígido. Recomendo que você instale o Windows
ANTES de instalar o Linux, em especial se for Windows 95/98/ME.

NÃO crie nenhuma partição para o Linux através do fdisk do DOS. Deixe o espaço
não-particionado e este será usado posteriormente no programa de instalação do
linux.

Particionamento não-destrutivo
------------------------------

Se você já tem o Windows instalado e configurado e não quer reinstalar tudo,
você pode usar o FIPS (que foi copiado para o disquete de inicialização) ou
outro programa que faça este trabalho (como o PartitionMagic). A maioria das
distribuições, como já foi mencionado, possui uma interface gráfica e intuitiva
para fazer isto, mas se não tiver, ou se por algum motivo você preferir fazer de
outra forma aqui está descrito como.

AVISO: O FIPS só funciona com partições FAT16 ou FAT32 (DOS, Windows 95/98/Me).
Não é possível usá-lo com partições NTFS (Windows NT/2000 e XP)

- Em primeiro lugar certifique-se de ter um disco de inicialização do DOS
(criado anteriormente) COM os arquivos fips.exe e restorrb.exe
- Verifique se seu disco rígido não tem erros. Isto pode impedir que ele seja
particionado, formatado e usado adequadamente.
- Faça uma desfragmentação completa usando o Desfragmentador do Windows
(Iniciar/Programas/Acessórios/Ferramentas de Sistema/Desfragmentador de disco)
ou outro programa similar. Isto irá mover todos os seus dados e programas que em
geral ficam espalhados, para o início do disco. Este espaço que ficar livre,
poderá ser usado para criar a segunda partição.
- Reinicie o computador com o disco contendo o FIPS imediatamente, para evitar
que dados sejam gravados desnecessariamente para o espaço que acabou de ser
liberado.
- Execute o FIPS e selecione qual partição deseja redimensionar. Escolha o
tamanho que quer usar para o Linux (mas lembre-se de deixar um espaço extra para
o Windows) de acordo com o que foi planejado anteriormente.
- O FIPS verificará se é possível redimensionar as partições da forma que você
deseja e irá perguntar se você deseja realmente prosseguir. Ele irá lhe dar a
oportunidade de salvar uma cópia das informações de particionamento anteriores
no disquete, para o caso de você precisar recuperar o esquema antigo em caso de
erro (usando o restorrb.exe).
- Antes de fazer qualquer coisa após redimensionar as partições e sair do FIPS,
reinicie o computador.
- Verifique com o SCANDISK se a sua antiga partição Windows (C:) está em
perfeitas condições e depois inicialize o sistema no Windows. Abra alguns
programas pra ver se está tudo OK.
- Se por algum motivo ocorrer qualquer erro, você pode restaurar o esquema
antigo usando o restorrb.exe e a imagem de particionamento gravada no disquete.
- Se tudo estiver bem, reinicie novamente usando o disquete de inicialização e
execute o programa FDISK. O FIPS dividiu sua partição primária do DOS em duas.
Você deve apagar a segunda, pois este espaço não particionado será usado agora
pelo Linux. Cuidado! Não apague a primeira partição (C:) ou poderá perdê-la e a
todos os seus dados.

Particionamento pelo Linux
--------------------------

Como já foi dito, quase todas as distribuições atuais permitem um
particionamento visual e intuitivo do disco. Este particionamento é feito como
parte do processo de instalação do linux (veja abaixo para maiores detalhes).

Você só precisa iniciar o instalador e ele irá perguntar (após fazer alguns
testes e algumas perguntas) se você deseja fazer o particionamento de forma
automática ou manual.

Se escolher a forma automática, ele irá utilizar o espaço em disco não-
particionado (que foi liberado anteriormente) ou se não encontrar, vai perguntar
se ele deve "pegar" o espaço necessário da partição Windows existente (se for
fazer isto, é recomendado fazer a verificação e desfragmentação do disco antes,
como explicado no item anterior).

Caso não seja possível usar nem o espaço não-particionado e nem o espaço
existente no Windows, ou ainda se você não quiser deixar o instalador
particionar automaticamente, você será apresentado à tela de particionamento
manual. Cada distribuição usa um esquema ligeiramente diferente, mas o princípio
é o mesmo.

Você precisará criar duas partições no mínimo. Uma chamada de swap, para a
memória virtual e outra chamada de "raiz" (ou "root", "/") que é onde serão
instalados todos os arquivos e programas. A ordem em que são criadas não é muito
importante.

Adicione uma partição swap primeiro. O tipo deve ser "linux-swap" ou "swap" e
ela não tem um "ponto de montagem". Selecione "formatar" (a menos que já esteja
usando esta partição como swap em outro linux) e escolha o tamanho. Como
mencionado, o tamanho pode variar e existem  várias "preferências" de acordo com
quanto você vai exigir da máquina (e quantos programas vai manter aberto). Se
tiver menos do que 128MB é bom criar uma partição com o dobro do tamanho da
memória ou até mais. Por exemplo 64MB de memória RAM + 128MB de swap. Se tiver
128MB ou 256MB, um swap com o mesmo tamanho da memória é recomendado. Se tiver
mais do que isso, pode criar uma com o mesmo tamanho da memória ou até menor.
Estes são apenas valores "chutados". Na prática, você teria que determinar
quanto de memória total os programas que você vai usar ocupam, e subtrair este
valor do tanto que possui de memória RAM.

Por exemplo, se vai rodar diversos programas ao mesmo tempo, que chegam a ocupar
até 300MB de memória e você possui 128MB de memória física, seria bom criar um
swap de no mínimo 200MB, num total de 328MB (com uma memória extra de reserva).

Depois de criar a partição de swap, você deve criar uma partição para o Linux.
Você pode usar todo espaço disponível para isso. O ponto de montagem é / (raiz,
root) e o tipo deve ser linux-native, ext2 (se precisar manter compatibilidade)
ou ext3 (se for uma distribuição mais atual e com um kernel mais moderno).
Marque a opção formatar.

Pronto, o particionamento está feito. Veja na instalação os outros passos para
instalar.

Instalando o Linux
------------------

OBS: Este é um guia geral de instalação que deve servir para a maioria das
distribuições. Algumas distribuições de linux usam modelos de instalação
específicos, voltados para usuários mais avançados ou mesmo para usuários mais
novatos. Por favor, consulte o guia da distribuição que escolheu, e se ele não
estiver disponível procure na internet. Se não conseguir ou então preferir não
seguir qualquer guia além deste, aja por sua própria conta e risco.

Até agora estivemos nos preparando para instalar o Linux. Nenhum dos passos
executados até aqui é exclusivo do Linux. Muitos deles servem para outros
sistemas operacionais, até mesmo para o Windows, se houver outros sistemas
instalados, mas a maioria das pessoas parece se esquecer disto. Instalar o Linux
não é muito diferente de instalar outros sistemas "mais fáceis".

0. Tenha em mãos todos os CDs da distribuição que pretende instalar, mais o
disquete de inicialização (caso não consiga dar boot pelo CD) e as informações
do seu computador obtidas logo no início. É bom ter as instruções de instalação
específicas da distribuição impressas (além destas que está lendo, se preferir)
ou disponíveis para serem lidas em outro computador (pro caso de não conseguir
reiniciar o seu).

1. Certifique-se de que todos os seus periféricos (teclado, mouse, drives
externos, modem, placa de rede, impressora, scanner, etc) estejam conectados ao
seu computador e LIGADOS. Isto permitirá uma detecção automática de todos os
dispositivos já na instalação, embora seja possível ativá-los manualmente depois
(o que pode dar um pouco mais de trabalho).

2. Comece inserindo o primeiro CD (ou o único!) no primeiro drive de CD (se
tiver mais de um). Insira também o disquete de inicialização do linux (se for
necessário) e reinicie a máquina. O linux deve ser iniciado automaticamente sem
você precisar fazer nada. Em alguns casos você deve selecionar um tipo
específico de inicialização. Experimente apenas pressionar ENTER e continuar com
a inicialização padrão. Isto deve funcionar em 99% dos casos. Se ocorrer algum
problema, talvez você precise criar algum disco de inicialização específico
(veja acima) ou passar parâmetros especiais para o kernel. Consulte o guia de
instalação para maiores detalhes.

3. O Linux irá detectar todo hardware presente em sua máquina. A primeira tela
que aparecer deverá ser uma seleção de idiomas, selecione Português/Brasil
(Brazilian Portuguese) se estiver disponível ou outro de sua preferência. OBS:
Muitos pacotes infelizmente só estão disponíveis em inglês, mas a maioria é para
usuários mais avançados de qualquer forma.

4. Em seguida o instalador pode perguntar qual o tipo de teclado e mouse
(serial, PS/2, USB, microsoft) e layout de teclado (us, us-
acentos/internacional, abnt2) você está usando.

5. Você será apresentado a uma tela para selecionar o tipo de instalação que
deseja (mínima, típica/padrão, completa, personalizada) e algumas opções
avançadas, como por exemplo, se deseja selecionar pacote por pacote a ser
instalado e se quer particionar o disco manualmente.

6. O próximo passo será particionar e formatar as partições. Siga as instruções
descritas anteriormente e vá para o próximo passo. A formatação das partições
pode demorar um pouco dependendo do tamanho e da velocidade do disco.

7. Uma seleção geral dos pacotes a serem instalados será exibida. Escolha de
acordo com suas necessidades (e disponibilidade de espaço) e continue. A partir
de agora deve ser iniciada a cópia dos pacotes. Esta é a parte mais demorada e o
tempo estimado depende do número de pacotes selecionados e da velocidade de seu
disco. Pode levar de 5 minutos a algumas horas. Aproveite para ler a respeito da
configuração da distribuição que está instalando ou mesmo fazer outra coisa.
Pode ser necessário também trocar os CDs durante a instalação, se houver mais de
um. Fique atento a este detalhe, para não perder tempo.

8. Copiados os pacotes, algumas configurações finais são necessárias:

- Definir uma senha para o usuário "root" que tem privilégios de administrador.
Não esqueça esta senha. Você pode anotá-la e guardá-la em um local seguro se
preferir. Evite usar o usuário root.
- Crie um usuário comum com seu nome e uma senha de sua escolha. É arriscado
usar o usuário root para as operações comuns do dia a dia.
- Configure a placa de vídeo e monitor usados pelo seu gerenciador de janelas.
Em geral isto é detectado automaticamente. Você pode simplesmente confirmar se
estiver tudo OK. Alguns monitores mais antigos, precisam de alguns ajustes
manuais (frequência do monitor, resolução máxima, etc). Consulte o manual do seu
monitor e da placa de vídeo.
- Configuração de rede, internet, impressoras e scanners. O Linux detecta
automaticamente a maioria destes dispositivos se estiverem ligados e você só
precisa fazer um "ajuste fino" em alguns casos. Se estiverem desligados, será
preciso configurá-los manualmente. Alguns deles podem ser detectados
posteriormente na inicialização por um programa de detecção de hardware
especial.
- Criação do disco de inicialização. É bom criar um disco de emergência do linux
(conhecido como rescue) para o caso de não conseguir inicializar diretamente
pelo disco rígido. (Por exemplo, se você instalar o Windows DEPOIS do linux.)
- Configuração do modo de inicialização. O Linux precisa de um programa
especial, chamado gerenciador ou carregador de boot para ser inicializado. Este
gerenciador pode permitir inclusive que você inicialize através de outro sistema
operacional (é assim que poderá continuar usando o Windows). Você pode
geralmente escolher entre o GRUB e o LILO. Se lhe for perguntado onde instalar o
gerenciador de boot, escolha o registro mestre de inicialização (Master Boot
Record, MBR) e escolha qual sistema deseja que inicialize como padrão
(possivelmente o windows).
- A maioria das distribuições tem estes passos, se houver mais alguma coisa a
fazer, siga conforme as instruções da sua distribuição.

9. A esta altura seu sistema deve estar pronto para iniciar no Linux. Remova
todos os CDs e disquetes dos drives e reinicie.

10. Agora seu sistema deve apresentar uma tela de seleção de boot. Você pode
entrar no Windows agora só pra ter certeza de que tudo está OK.

11. Depois, reinicie e inicie o sistema no Linux. Se tudo correr bem, o sistema
irá carregar sem problemas e uma tela pedindo seu nome de usuário (login) e
senha (password) será apresentada. Digite o nome de usuário que criou na
instalação (não é recomendado entrar como "root" a não ser em emergências e
casos especiais) e sua respectiva senha. Selecione o gerenciador de janelas a
ser usado (possivelmente: KDE, Gnome ou WindowMaker) e pronto. Você já está
usando linux! Se ocorrer algum problema na inicialização, tente inicializar no
modo texto (modo console) se estiver disponível ou use o disco de recuperação
criado (ou o próprio CD de instalação talvez tenha uma opção destas). Assim
poderá verificar onde está o problema. Procure ajuda se necessário (veja
abaixo).

12. É possível que algum dispositivo não tenha sido adequadamente detectado e
você precise configurá-lo manualmente (exemplo: placa de som, impressora, etc.).
Cada distribuição possui um modelo diferente para configuração, mas a maioria
usa o "linuxconf" ou um programa com nome semelhante a "Control Center" ou
"Config" (por exemplo: Mandrake Control Center). Procure por este programa no
menu de aplicativos ou na própria área de trabalho e veja se acha a configuração
dele. Como eu falei, cada distribuição usa um esquema diferente e você deve
procurar o guia da sua para configurar os dispositivos faltantes.

13. Algumas placas e dispositivos mais "exóticos" podem não ser
detectados/configurados automaticamente e você pode precisar até mesmo obter
drivers para eles. Procure informações e ajuda na internet ou com algum colega,
mas antes de sair perguntando pra todo mundo: LEIA A DOCUMENTAÇÃO!!! 98% das
dúvidas já estão respondidas lá. E importante: se for pedir ajuda em algum
fórum, lista de discussão, mailing list, newsgroup ou mesmo para algum amigo,
por e-mail, etc, seja educado (ninguém vai se preocupar em ajudar alguém sem
educação, ainda mais por ser uma ajuda voluntária), seja paciente (não adianta
escrever URGENTE, PROBLEMA ou ERRO em uma mensagem que a maioria vai ignorar) e
procure fornecer o máximo possível de informações sobre o seu sistema para que
seja mais fácil identificar o problema. Se possível descreva resumidamente o
problema já no assunto da mensagem. Exemplos: "Problema com placa de vídeo SiS
620", "Kernel panic durante a inicialização do dispositivo XYZ", "Demora na
inicialização do Mandrake 9.1, kernel 2.4.21, KDE 3", etc. Isto irá chamar a
atenção de pessoas que já tiveram problemas semelhantes. No corpo da msg dê mais
detalhes:

> ''Acabei de instalar a distribuição BANANA 3.2b e não estou conseguindo
> configurar minha placa de rede LARANJA, com chipset MADE IN ELBONIA. Estou
> usando o kernel 2.4.17 e já tentei configurar pelo Linuxconf, mas ele dá a
> seguinte mensagem de erro: "XYZBLAH!: No such device. Try to use parameters
> ABC." O que significa isso?
> 
> Mais detalhes do meu computador:<br>
> Wintel Lenthium 2.0Ghz + 12MB de RAM<br>
> Placa-mãe JABUTICABA<br>
> Placa de rede LARANJA, modelo HIJ, slot PCI
> 
> Uso também o Windoze 3000 Pro mas a placa funciona perfeitamente nele. O que
> fazer?''

Se alguém pedir mais informações, vc pode verificar como foi a inicialização do
seu sistema usando um programa chamado "dmesg". Abra um terminal e digite "dmesg
| less" para ver linha por linha de tudo o que o linux detectou e fez durante a
inicialização. Você pode gravar a saída num arquivo com "dmesg > my_dmesg.txt" e
mostrar para alguém que entenda se é possível identificar o problema através
dele.

14. Internet:

- Se você acessa internet por linha discada, procure pelo KPPP, que é um
discador semelhante ao do Windows. Se não conseguir conectar, seu modem pode não
ter sido reconhecido corretamente pelo Linux. Procure descobrir qual o modelo e
fabricante e se não é um WinModem (ou SoftModem) e ajuda de como configurá-lo no
linux. É claro, você deve se certificar que ele funciona normalmente no Windows.

- Se você acessa por uma conexão de banda larga (via cabo, ADSL, rádio,
satélite) provavelmente só precisa configurar a placa de rede. Se sua placa de
rede for detectada automaticamente não será muito mais complicado do que no
próprio Windows, basta selecionar as opções e preencher os campos corretamente.

15. Resta agora começar a explorar e se acostumar com o novo sistema. Há
centenas de tutoriais disponíveis na internet (e possivelmente no próprio CD que
você usou para instalar).

16. Dicas:

- Reiniciar o servidor X: CTRL+ALT+BACKSPACE
- Ir para o modo console (texto): CTRL+ALt+F2
- Voltar para o modo gráfico: CTRL+ALt+F7
- Se iniciar o sistema já no modo texto, após fazer o login, digite no prompt de
comando "startx", "kde" ou "gnome" para entrar no modo gráfico.
- Se esquecer a senha do seu usuário, entre como root, abra um terminal, execute o
comando "passwd nome_do_usuario" e digite a nova senha. Se esquecer a senha
root, você precisará iniciar o sistema através de um disco de recuperação para
alterá-la.

Boa sorte!
