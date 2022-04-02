Processos
---------

- Processo e Job
- Seção de texto, Contador de programas, Registradores, Pilha, Seção de dados
- Estados: Novo, Em execução, Em espera, Pronto, Encerrado
- Bloco de Controle de Processo (PCB): Estado do processo, Contador do programa, Registradores de CPU, Informações de escalonamento de CPU, de gerência de memória, de contabilização, de E/S
- Escalonamento de processos:
    - Filas de escalonamento
    - Escalonador (curto, médio e longo prazo)
    - Troca de contexto
- Operações: Criação (pai, filho, estrutura em árvores), Término
- Comunicação entre processos (IPC): memória compartilhada, mensagens, sincronização

Threads
-------

- Processo leve, diversos fluxos de controle
- Benefícios: capacidade de resposta, compartilhamento de recursos, economia, utilização de arquiteturas multiprocessador.

Escalonamento de processos
--------------------------

- Surtos de I/O e CPU
- Escalonador de CPU, Escalonamento preemptivo, Dispatcher (Despachante)
- Critérios de escalonamento: utilização de CPU, throughput, tempo de retorno, de espera e de resposta.
- Algoritmos: first-come, first-served, job mais curto primeiro, por prioridade, round-robin, múltiplas filas, tempo real
- Escalonamento de threads

Sincronização de processos
--------------------------

- Condição de corrida
- Seção crítica
- Hardware de sincronização
- Semáforos
- Monitores

Deadlocks
---------

- Recursos
- Condições para ocorrer deadlock: exclusão mútua, posse e espera, não-preempção, espera circular
- Tratamento de deadlocks: prevenção, impedimento, detecção, recuperação
