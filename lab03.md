Laboratório 3: Utilização do modo console (texto) do Linux
==========================================================

Comparações
-----------

Vamos usar o termo "diretórios" para nos referirmos àquilo que chamamos de
"pastas" no Windows. No linux (como em todo sistema unix) não existem "unidades"
ou "drives" e sim uma única árvore de diretórios que começa pela raiz (root,
representada pela barra "/"). A barra ("/", também chamada de slash) também
serve para separar os nomes dos diretórios e arquivos, sendo que no Windows usa-
se a barra invertida ("\", backslash).

Os nomes de arquivos no Linux seguem uma convenção semelhante à do Windows,
podendo ter espaços (neste caso, deve-se usar sempre aspas), letras, números e
alguns caracteres especiais. Certos caracteres não são permitidos por terem um
significado especial (por exemplo: * e ?).

No linux maiúsculas e minúsculas fazem diferença em quase tudo, desde nomes de
usuários, arquivos e diretórios, até nos parâmetros passados pros comandos.
Todos os comandos listados aqui devem ser digitados em letra minúscula ou não
funcionarão.

Acessando o modo console
------------------------

Você pode testar estes comandos em uma janela de terminal (konsole, xterm,
gterm, etc). Isto permite que você continue trabalhando com as outras janelas do
modo gráfico (XFree).

Se preferir entrar diretamente no modo console, pressione CTRL+ALT+F2 e para
voltar ao modo gráfico pressione CTRL+ALT+F7. Neste caso, você vai precisar
digitar um login e senha que é o mesmo do modo gráfico. Você pode até mesmo
manter mais de um console aberto (virtual consoles). Para alternar entre eles
use ALT+F1, ALT+F2, etc.

Sumário dos principais comandos do shell
-----------------------------------------

A maioria dos comandos possuem um sistema de ajuda. Experimente usar
"*nomedocomando* --help" para ver uma breve explicação do que ele faz e uma
listagem dos principais parâmetros. Para uma ajuda mais aprofundada, digite
"man *nomedocomando*" para ver seu manual. Muitos comandos tem inclusive tem um
sistema de ajuda mais completo. Entre com o comando "info" para conhecer este
sistema de ajuda.

`clear` - Limpa (clear) a tela

`pwd` - Mostra o diretório atual (Print Work Directory)

`uname` - Mostra informações do sistema atual.
Exemplos:

~~~sh
uname -a # Mostra informações mais completas, inclusive versão do kernel.
~~~

`dmesg` - Mostra uma série de informações da inicialização do sistema (detecção de
dispositivos, etc). Pode ser muito útil para identificar problemas. Exemplo de
uso:
  
~~~sh
dmesg | more    
-ou-
dmesg | less
~~~

`uid` - Mostra informações sobre a sua identificação.

`whoami` - Mostra quem é você (seu usuário).

`date` - Mostra data e hora atual.

`free`, `df`, `du` - Mostra informações de espaço livre e utilizado de memória e
disco.

`ls` - Lista (list) os arquivos do diretório atual

Parâmetros:

-a : mostra todos os arquivos, inclusive os ocultos (all)

-l : listagem detalhada (longa)

-F : mostra um símbolo junto com o nome do arquivo indicando seu tipo (/=
diretório, *=executável, ~=backup)

-R : mostra inclusive os sub-diretórios (R: recursive)

É possível combinar vários parâmetros numa chave só: -la ou -aFl

Obs: Você pode usar um asterisco (*) para substituir partes do nome do
arquivo. Para listar todos os arquivos que começam com a letra "A" e terminam
com a letra "o", use "A*o". Se usar apenas "*" serão exibidos todos os
arquivos. Use uma interrogação (?) se quiser substituir apenas um caractere.
Estes caracteres especiais (e mais outros) podem ser usados em outros comandos
que envolvem arquivos. Ex:

mari? - Pode substituir: mario, maria, mari1 ou qualquer outra coisa que
comece com "mari" e tenha mais um caracter.

*.txt - Substitui qualquer coisa que termine com "*.txt": a.txt, doc.txt,
carta.txt, etc.

---

`cd` - Muda o diretório de trabalho (Change Directory)
Exemplos:

~~~sh
cd teste               # Muda para o sub-diretório "teste"
cd /home/usuario/teste # Muda para o sub-diretório "teste" que está dentro do diretório "/home/usuario".
cd /                   # Muda para o diretório raiz (root, "/")
cd ..                  # Volta um "nível" de sub-diretório.
cd .                   # "Muda" para o diretório atual
cd ~                   # Volta para o diretório do usuário (home)
~~~

---

`mkdir` - Cria um diretório (Make Directory)
Exemplos:

~~~sh
mkdir teste     # Cria um sub-diretório chamado "teste", dentro do diretório atual.
mkdir teste/sub # Cria um sub-diretório "sub" dentro do diretório "teste".
~~~

`rmdir` - Apaga um diretório (Remove Directory). Este precisa estar vazio para ser
apagado.
Exemplo:

~~~sh
rmdir teste # Apaga o diretório "teste"
~~~

`cp` - Copia arquivos (Copy)
Exemplos:

~~~sh
cp texto texto2 # Faz uma cópia do arquivo "texto" para o arquivo "texto2".
cp texto teste  # Se "teste" for um diretório (criado acima), copia o arquivo texto para dentro do diretório teste com o mesmo nome.
~~~

`mv` - Mover arquivos (Move). Também usado para renomear.
Exemplos:

~~~sh
mv arq1.c /tmp     # Move o arquivo arq1.c para o diretório "/tmp"
mv prog.c hello.c  # Muda o nome do arquivo "prog.c" para "hello.c"
mv teste diretorio # Se "teste" for um diretório, renomeia-o para "diretorio".
~~~

`rm` - Apagar arquivos (Remove)
Exemplo:

~~~sh
rm hello.c    # Apaga o arquivo com o nome "hello.c"
rm *.c        # Apaga todos os arquivos que terminam com ".c"
rm -Rf inutil # Remove o diretório "inutil" com todos os seus arquivos (R: recursive) mesmo que não esteja vazio (f: force)

`cat` - Exibe o conteúdo de um (ou mais) arquivos (conCATenate)
Exemplo:

~~~sh
cat texto1 texto2 texto3 # Exibe os 3 arquivos como se fossem um só
cat texto* # Exibe todos os arquivos que começam com "texto"
~~~

OBS: Você pode usar o cat para criar arquivos texto rapidamente. Ele não é um
editor completo, mas pode ajudar em alguns casos. Digite:

~~~sh
cat > teste.txt
~~~

Após isso, digite quanto texto quiser e quando terminar pressione CTRL+D (^D). Você poderá verificar o que foi escrito com "cat teste.txt".

`more` / `less` - Exibe o conteúdo de um arquivo página por página.
Exemplo:

~~~sh
more texto
less documento
~~~

OBS: Você pode usar more/less combinado com outros comandos, por exemplo:
     
~~~sh
cat texto* | more
ls /etc | less
~~~

`wc` - Conta o número de palavras, caracteres e linhas da entrada. Pode ser usado
em conjunto com outros programas. Exemplo

~~~sh
cat teste.txt | wc
~~~

Exercícios
----------

A partir do seu diretório "home" (/home/*nomeusuario*) faça os seguintes
exercícios:

1. Certifique-se de que está em seu diretório home com o "pwd". Caso não esteja,
entre com o comando "cd" ou "cd ~" para voltar para seu diretório.

2. Crie alguns sub-diretórios (mkdir) e mova-se através deles (cd, pwd, ls).
Apague alguns deles (rmdir).

3. Crie alguns arquivos de teste com o comando "cat >". Experimente os comandos
para copiar, mover, apagar com estes arquivos.

4. Explore os diretórios do sistema. Vá para a raiz (cd /) e comece a navegar
pelos principais diretórios (etc, bin, usr, tmp, home...). Você pode ler o
conteúdo de alguns arquivos usando o "cat" e procurar por alguma documentação no
diretório /usr/doc.

5. Examine a ajuda dos principais comandos aprendidos, usando "*comando* --help"
e/ou "man *comando*".

6. Consulte o manual de usuaário do Conectiva Linux online na seção "modo
texto": <http://www.conectiva.com/doc/livros/online/9.0/usuario/>
A Techlinux (outra distribuição brasileira) também disponibiliza seu manual para
consulta online: <http://www.techlinux.com.br/data/docs/guia-tech30/> (veja o
capítulo 7 - Comandos do modo texto - na página 101).

7. Procure o tutorial (HOW-TO) [DOS-Win-to-Linux-HOWTO](https://tldp.org/HOWTO/DOS-Win-to-Linux-HOWTO-1.html) se você já usou o DOS e
quer aprender alguns comandos mais avançados.
