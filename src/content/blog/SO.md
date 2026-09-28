---
title: "Sistemas Operacionais: Notas e Resumos (OSTEP)"
description: "Resumo dos principais conceitos baseados em Operating Systems: Three Easy Pieces: processos, chamadas de sistema, escalonamento, concorrência, travas e semáforos."
pubDate: 2026-09-28
tags: ["Sistemas Operacionais", "Concorrência", "Processos", "Kernel"]
draft: false
---

# *Operating Systems: Three Easy Pieces*

### **Capítulo 4: Abstração de Processos**
* **Definição de Processo:** É a abstração de um programa em execução no sistema.
* **Espaço de Endereçamento (Imagem em Memória):**
  * **Código (*Text*):** Instruções em linguagem de máquina do programa executável.
  * **Dados Estáticos (*Data*):** Variáveis globais e estáticas.
  * **Heap:** Região de memória dinâmica alocada explicitamente pelo programador em tempo de execução (ex.: `malloc`).
  * **Pilha (*Stack*):** Armazena variáveis locais, parâmetros de funções e endereços de retorno, crescendo em sentido oposto ao Heap.
* **Estados do Processo:**
  * **Executando (*Running*):** O processo está utilizando a CPU no momento.
  * **Pronto (*Ready*):** O processo está pronto para executar, aguardando ser escolhido pelo escalonador.
  * **Bloqueado (*Blocked*):** O processo está suspenso aguardando a conclusão de um evento externo ou operação de E/S.
* **Bloco de Controle do Processo (PCB):** Estrutura de dados interna do kernel (`struct proc`) que armazena o identificador (PID), o estado atual e o contexto de registradores salvos durante uma troca de contexto.

---

### **Capítulo 5: API de Processos (Chamadas de Sistema no UNIX)**
* **`fork()`:** Duplica o processo chamador para criar um novo processo filho. Retorna `0` para o filho e o PID do filho para o pai.
* **Isolamento de Memória:** O `fork()` cria um espaço de endereçamento isolado para o filho. Modificações em variáveis realizadas pelo filho não afetam a memória do pai.
* **`wait()` / `waitpid()`:** Suspende a execução do processo pai até que o processo filho seja concluído, garantindo uma ordem determinística de execução. Sem essa chamada, a ordem de execução fica a critério não-determinístico do escalonador de CPU.
* **`exec()`:** Reescreve o espaço de memória (código, dados, pilha e heap) do processo atual com um novo programa executável sem alterar o seu PID.

---

### **Capítulo 7: Escalonamento de CPU**
* **Tipos de Escalonadores:**
  * **Não-Preemptivo:** O processo executa até ser concluído ou ceder a CPU por conta própria ao realizar uma chamada de E/S.
  * **Preemptivo:** O sistema operacional pode interromper forçadamente o processo atualmente em execução para atribuir a CPU a outro processo, utilizando interrupções de temporizador do hardware (*timer interrupts*).
* **Métricas de Escalonamento:**
  * **Tempo de Retorno (*Turnaround Time*):** \\(T_{retorno} = T_{conclusão} - T_{chegada}\\). Mede a rapidez total de conclusão de uma tarefa.
  * **Tempo de Resposta (*Response Time*):** \\(T_{resposta} = T_{primeira\_execução} - T_{chegada}\\). Mede a rapidez do sistema em fornecer o primeiro atendimento/resposta.
* **Políticas Principais:**
  * **SJF (*Shortest Job First*):** Executa primeiro os processos mais curtos. É ótimo para minimizar o tempo médio de retorno em cargas que chegam simultaneamente.
  * **STCF (*Shortest Time-to-Completion First*):** Versão preemptiva do SJF. Interrompe o processo atual caso um novo processo chegue com tempo restante menor.
  * **Round Robin (RR):** Alterna o uso da CPU entre os processos prontos em fatias fixas de tempo (*time-slice* ou *quantum*). Otimiza o tempo de resposta, mas apresenta fraco desempenho quanto ao tempo de retorno.
* **Trade-offs de Time-Slice:** *Time-slices* muito curtos melhoram a responsividade, mas aumentam o *overhead* devido a trocas de contexto frequentes. *Time-slices* muito longos reduzem a sobrecarga, porém pioram a interatividade.
* **Inanição (*Starvation*):** Fenômeno em que um ou mais processos prontos nunca recebem tempo de CPU devido à priorização constante de outros processos pelo escalonador.

---

### **Capítulo 26: Concorrência - Introdução**
* **Definição de Thread:** É uma linha de execução independente dentro de um processo. Threads do mesmo processo compartilham o mesmo espaço de endereçamento (código, dados e heap), mas possuem registradores, contador de programa (PC) e **pilha (*stack*) própria**.
* **Região Crítica (*Critical Section*):** Trecho de código que acessa um recurso ou variável compartilhada e que não deve ser executado por múltiplas threads simultaneamente.
* **Condição de Corrida (*Race Condition*):** Situação de erro em que o resultado final da execução varia imprevisivelmente de acordo com a ordem de execução das threads concorrentes.
* **Exclusão Mútua (*Mutual Exclusion*):** Garantia de que apenas uma thread/processo executa dentro de uma região crítica por vez.

---

### **Capítulo 27: API de Threads (Pthreads)**
* **Criação e Espera:** Uso das chamadas `pthread_create()` para iniciar threads e `pthread_join()` para aguardar o seu término.
* **Sincronização:** Utilização de travas do tipo *mutex* (`pthread_mutex_lock` / `pthread_mutex_unlock`) para garantir a exclusão mútua e variáveis de condição (`pthread_cond_wait` / `pthread_cond_signal`) para suspender e despertar threads com base no estado de variáveis.

---

### **Capítulo 28: Travas (*Locks*)**
* **Suporte de Hardware:** Instruções atômicas como *Test-And-Set* e *Compare-And-Swap* permitem testar e alterar variáveis de controle sem interrupções. *Fetch-And-Add* viabiliza travas baseadas em senha (*Ticket Locks*), garantindo ordem e evitando inanição.
* **Spinlocks:** Tipo de trava em que a thread aguarda em um loop ativo (*spin-wait*) até a liberação do recurso, o que desperdiça tempo de CPU.
* **Evitando o *Spinning* com o SO:** Chamadas como `yield()` cedem a CPU voluntariamente. Mecanismos avançados no kernel (como `futex` no Linux ou `park`/`unpark` no Solaris) colocam as threads em filas de espera bloqueadas.

---

### **Capítulo 29: Estruturas de Dados Concorrentes**
* **Granularidade das Travas:**
  * **Trava Grossa (*Coarse-grained*):** Uma trava única protege a estrutura inteira. É simples, porém limita o paralelismo.
  * **Trava Fina (*Fine-grained*):** Usa travas independentes em subpartes da estrutura (ex.: por balde em tabelas hash ou por nó em listas), permitindo acessos simultâneos.
* **Contadores Aproximados (*Sloppy Counters*):** Estrutura escalável que utiliza contadores locais por CPU com atualizações periódicas em um contador global ao atingir um limiar (*threshold*), reduzindo a contenção de travas.

---

### **Capítulo 31: Semáforos**
* **Definição:** Primitiva de sincronização composta por um valor inteiro manipulado atômica e exclusivamente por `sem_wait()` (decrementa; se for negativo, bloqueia) e `sem_post()` (incrementa e desbloqueia).
* **Semáforo Binário (Mutex):** Inicializado com valor `1`, utilizado para impor exclusão mútua em regiões críticas.
* **Semáforo Contador e Sinalização:** Inicializado com `0` ou \\(N\\), utilizado para ordenar a execução entre threads (ex.: pai aguardando filho) ou para limitar recursos em buffers compartilhados (*Bounded Buffer*).

---

### **Capítulo 32: Bugs de Concorrência e Multiprocessamento**
* **Deadlock (Impasse):** Situação em que duas ou mais threads ficam travadas para sempre, pois cada uma mantém uma trava e aguarda pela trava possuída pela outra.
* **Prevenção de Deadlock:** A estratégia primária de prevenção consiste em impor uma **ordem global estrita para a aquisição de travas** no código.
* **Afinidade de Cache (*Cache Affinity*):** Manter a execução de uma thread/processo no mesmo *core* físico reutiliza os dados previamente carregados nas memórias cache locais (como a L3 compartilhada), reduzindo acessos à RAM e elevando o desempenho.

---
