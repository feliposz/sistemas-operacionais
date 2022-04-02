Memória virtual no Linux
------------------------

No Linux a memória virtual é implementada num esquema de paginação sob demanda.
Conforme visto em classe, este sistema trabalha com um arquivo ou dispositivo de
swapping, em que as páginas da memória são trocadas. Vamos ver aqui como é
possível criar um arquivo de swap adicional.

Criando um arquivo de swap "extra":

1. Entrar como usuário root e posicionar-se no diretório "/tmp".

~~~sh
cd /tmp
~~~

2. Criar um arquivo vazio já com o tamanho certo. Para isso vamos usar o comando
"dd":

~~~sh
dd if=/dev/zero of=tmpswap bs=1024 count=2048
~~~

Isto irá criar um arquivo contendo apenas zeros ("vazio") chamado tmpswap, de
exatamente 2MB. (1024 bytes x 2048 = 2MB)
(bs = tamanho do bloco em bytes e count = quantidade de blocos a gravar.
/dev/zero é um dispositivo especial que sempre que for lido retornará o valor
zero.)

3. Preparar o arquivo para ser usado como swap.

~~~sh
mkswap tmpswap
~~~

4. Verificar o espaço de swap disponível com o comando "free".

~~~sh
free
~~~

5. Habilitar o novo swap "extra".

~~~sh
swapon tmpswap
~~~

6. Verificar novamente o espaço de swap disponível com o comando "free". Desta
vez deve haver aprox. 2MB a mais disponível.

7. Desabilitar o swap.

~~~sh
swapoff tmpswap
~~~

8. Apague o arquivo temporário.

~~~sh
rm tmpswap
~~~

O swap "oficial" sendo usado está obviamente em uma partição separada. Você pode
ver qual é observando o arquivo /etc/fstab.


Criando um sistema de arquivos
------------------------------

Vamos fazer uma experiência semelhante ao da criação do swap "extra" aqui.

1. Novamente é preciso estar como root e preferencialmente no diretório "/tmp".

2. Usamos o comando "dd" novamente, mas vamos criar um arquivo maior:

~~~sh
dd if=/dev/zero of=tmpfs bs=1024 count=20480
~~~

Irá criar um arquivo com 20MB.

3. Criar um sistema de arquivos neste arquivo criado. OBS: Normalmente, criamos
um sistema de arquivos em uma partição ou dispositivo, mas neste caso, como é um
teste, usamos um arquivo comum.

~~~sh
mkfs -t ext2 tmpfs
~~~

"-t ext2" faz com que o comando mkfs (make filesystem) crie um sistema de
arquivos ext2 ("padrão" do linux).

4. Criar um diretório e montar o sistema recém-criado neste diretório.

~~~sh
mkdir tmpmnt
mount -o loop tmpfs tmpmnt
~~~

OBS: O parâmetro "-o loop" é necessário por "tmpfs" ser um arquivo e não um
dispositivo.

5. Agora acesse o diretório e copie algum arquivo para o novo sistema de
arquivos. Apenas para testá-lo.

~~~sh
cd tmpmnt
cp /etc/passwd .
ls
~~~

6. Saia do diretório, desmonte o sistema de arquivos e apague o arquivo.

~~~sh
cd ..
umount tmpmnt
rm tmpfs
~~~

Criando programas em C no Linux
-------------------------------

Crie um arquivo "ola.c" usando qualquer editor de sua preferência (o kedit por
exemplo) e salve-o em seu diretório de trabalho (/home/aluno). O programa deve
ser assim:

~~~c
#include <stdio.h>

int main()
{
	printf("Olá mundo!\n");
	return 0;
}
~~~

Abra um terminal e a partir do seu diretório de trabalho execute o seguinte
comando:

~~~sh
gcc -o ola ola.c
~~~

Este comando irá compilar o arquivo-fonte "ola.c" para um arquivo executável do
linux "ola". Para executar este novo programa digite:

~~~sh
./ola
~~~

Para fazer mais testes de programação, veja os exemplos abaixo que tratam de
criação de processos e trabalho com arquivos.

~~~c
/************** proc1.c **************/

#include <stdio.h>
#include <unistd.h>

int main()
{
	int pid;

	/* fork cria uma cópia do processo que chamou,
	   ambas as cópias continuam do mesmo ponto, ou seja
	   depois da chamada a fork */
	pid = fork();
        /* no pai o valor de retorno é o pid do filho */
	if (pid != 0)
		printf("Mensagem impressa pelo pai (%d)\n", pid);
	else /* no filho é sempre zero */
		printf("Mensagem impressa pelo filho (%d)\n", pid);

	return 0;
}

/************** proc2.c **************/

#include <stdio.h>
#include <unistd.h> /* funções fork, wait e execve */

int main()
{
	int pid;

	pid = fork();
	if (pid != 0) {
		printf("Pai: pid do Filho = %d\n", pid);
		wait(NULL); /* espera o filho terminar */
		printf("Pai: Filho terminou\n");
	} else {
		printf("Filho: inicio\n");
		execve("/bin/date", NULL, NULL);
		printf("Filho: Erro na execução de execve\n");
 		/* "execv"e executa ou programa substituindo a
		   imagem atual do processo na memória. A função
		   nunca retorna, exceto em caso de erro. */
	}

	return 0;
}

/************** proc3.c **************/

#include <stdio.h>
#include <unistd.h>

int main()
{
	int pid;

	pid = fork();
	if (pid != 0) {
		printf("Pai: pid do Filho = %d\n", pid);
		sleep(2); /* espera 2 segundos */
		kill(pid); /* e mata processo filho */
		printf("Pai: Filho terminou\n");
	} else {
		printf("Filho: inicio\n");
		execve("/usr/bin/yes", NULL, NULL);
		printf("Filho: Erro na execução de execve\n");
	}

	return 0;
}

/************** arq1.c **************/

#include <stdio.h>
#include <stdlib.h>

int main()
{
	FILE *fp;
	int c;
	char str[20];

	/* abre um arquivo para gravação */
	fp = fopen("teste.txt", "w");
	if (fp == NULL) {
		printf("Erro ao abrir arquivo para gravação.\n");
		exit(1);
	}
	fputc('O', fp); /* grava um caracter no arquivo */
	fputs("teste", fp); /* grava uma string no arquivo */
	fclose(fp);

	/* abre um arquivo para leitura */
	fp = fopen("teste.txt", "r");
	if (fp == NULL) {
		printf("Erro ao abrir arquivo para leitura.\n");
		exit(1);
	}
	c = fgetc(fp); /* lê um caracter do arquivo */
	fgets(str, 20, fp); /* lê uma string do arquivo */

	printf("Char = %c\n", c);
	printf("String = %s\n", str);

	return 0;
}

/************** arq2.c **************/

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main()
{
	char str[200];

	if (mkdir("testedir", 0777) != 0) {
		printf("Erro ao criar diretório.\n");
		exit(1);
	}
	chdir("testedir");
	getcwd(str, 200);
	printf("Current Working Directory = %s\n", str);
}
~~~
