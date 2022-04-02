Laboratório 2: Mais sobre o modo gráfico
========================================

Trabalhando com pastas e arquivos no konqueror
-----------------------------------------------

O Konqueror é o gerenciador de arquivos e navegador web do KDE (assim como o
Explorer e o Internet Explorer do Windows). Muitas das operações efetuadas nele
são semelhantes às do Explorer justamente para ajudar na familiarização.
Operações como clicar com o botão direito para abrir um menu de contexto, clique
ou clique-duplo para abrir, arrastar e soltar funcionam de forma idêntica na
maioria dos casos.

Experimente clicar com o botão direito sobre alguns arquivos e pastas e veja
suas propriedades.

Crie algumas pastas e arquivos de texto, com o botão direito do mouse e clicando
em Criar Novo/New.

> ATENÇÃO: O linux possui um controle de permissões mais rígido que o Windows.
Portanto, você não poderá apagar, criar ou alterar arquivos e pastas
(diretórios) fora do seu diretório de usuário (que deve ser
/home/*nomeusuario*). Somente o usuário administrador (root) tem acesso às
outras pastas, portanto, faça estas experiências dentro de sua pasta de usuário.

Usando disquetes e CDs
----------------------

No DOS e no Windows, os drives de disquete, CDs e outros dispositivos são
acessados através das unidades (A:, B:, C:, D:, etc). Tais unidades não existem
em sistemas unix. Usa-se em seu lugar um sistema de arquivos únicos, sendo que
estas unidades removíveis devem ser "montadas" em algum ponto desse sistema de
arquivos (normalmente, nos diretório /mnt/floppy, /mnt/cdrom, etc.).

Em alguns ambientes você pode acessar essas unidades, simplesmente clicando em
um ícone representando-o na área de trabalho. Em outros, você deve fazer a
"montagem" manualmente. Clicando com o botão direito e em "Montar/Desmontar"
(Mount/Unmount). Você pode ainda clicar com o botão direito na área de trabalho,
clicar em Criar Novo/New e no dispositivo Disquete ou CD-ROM para acessá-lo.

OBS: Não é recomendado remover disquetes dos drives sem antes desmontá-los, pois
em alguns casos o SO pode ter informações pendentes a serem gravadas que seriam
perdidas. O mesmo acontece com os drives de CD, mas neste caso a maioria dos
dispositivos já trava automaticamente não deixando você ejetar através do botão
da unidade. Neste caso, clique com o botão direito sobre o ícone do CD na área
de trabalho e depois em Ejetar/Eject.

Internet
--------

Você pode visitar um site da web com o Konqueror digitando
http://endereco.do.site na sua barra de localização. Veja informações da aula
anterior sobre como fazer para acessar a internet através do Proxy no
laboratório.

Para navegar no seu sistema de arquivos você usa file:/ no lugar de http://

Obtendo ajuda
-------------

O KDE possui um sistema de ajuda que pode ser bastante útil para iniciantes. Vá
no menu KDE e clique em Ajuda/Help. Há muitas dicas de como fazer desde as
operações mais fundamentais até algumas mais avançadas, dentro do ambiente do
KDE.

Exercícios
==========

1 - Crie a estrutura de pastas/diretórios a seguir, no seu diretório de usuário:

~~~
~ (o til representa sempre seu diretório de usuário)
|
+- tmp
|
+- textos
|
+- programas
    |
    +- c
    |
    +- pascal
~~~

2 - Crie os seguintes arquivos através do editor do KDE (KEdit ou KNotepad ou
Kate):

- Dentro da pasta "textos", crie um arquivo do tipo texto, com seu nome e mais
alguma informação que queira acrescentar
- Na pasta "programas/c", crie um arquivo texto chamado "hello.c" e digite o
seguinte nele:

~~~c
#include <stdio.h>

int main()
{
    printf("Hello World!\n");
    return 0;
}
~~~

3 - Faça algumas alterações na estrutura para praticar. Por exemplo: altere o
nome de alguns arquivos, mova-os através de arrastar e soltar (inclusive
selecionando vários de uma só vez). Faça cópia de alguns arquivos, apague outros
e use a lixeira para recuperá-los, etc.

4 - O KDE possui uma série de aplicativos básicos que já são instalados junto com
ele. Assim como os acessórios do Windows (Paint, Bloco de Notas, WordPad).
Procure os equivalentes destes aplicativos no KDE e ajuda de como usá-los na
documentação do KDE.

5 - Use o konqueror para acessar as seguintes páginas e conhecer mais sobre o KDE
e o Conectiva Linux:
http://www.kde.org/documentation/
http://www.conectiva.com/doc/livros/online/9.0/usuario/ (você pode consultar os
capítulos Conceito de Utilização, Interfaces Gráficas, Internet e Aplicativos do
Conectiva para saber mais)

