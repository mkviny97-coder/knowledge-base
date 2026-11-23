# Concorrência, Paralelismo e Sistemas Distribuídos

## Visão Geral

Teoria completa: modelos de thread, primitivas de sincronização, modelos de memória, estruturas lock-free, consenso (Paxos/Raft), actors, async/await, verificação formal, padrões distribuídos.

---

## Modelos de Thread

| Modelo | Descrição | Exemplos | Vantagens | Desvantagens |
|--------|-----------|----------|-----------|--------------|
| **1:1 (Kernel)** | Thread = OS thread | NPTL (Linux), Windows | Paralelismo verdadeiro, blocking simples | Overhead alto, escalabilidade limitada |
| **M:1 (Green)** | M user threads → 1 OS thread | Old Java, Go (antigo) | Baixo overhead, milhões de threads | Não usa multi-core, blocking bloqueia todos |
| **M:N (Hybrid)** | M user → N OS (work-stealing) | Go, Erlang, Rust async, Java Loom | Melhor dos dois mundos | Complexidade de runtime |

### Work-Stealing Scheduler
- **Deque por worker**: push/pop local (bottom), steal (top)
- **Cilk/Go/Tokio/.NET**: implementações produção
- **Work-first vs Help-first**: políticas de spawn

---

## Primitivas de Sincronização

### Spinlocks
- **TTAS** (Test-and-Test-and-Set): reduz tráfego de cache
- **Ticket Lock**: FIFO, fairness
- **MCS Lock** (Mellor-Crummey Scott): queue-based, local spinning, NUMA-friendly

### Mutex
- **futex** (Fast Userspace Mutex): kernel só em contenção
- **Adaptive Spinning**: spin curto antes de futex
- **Priority Inheritance**: evita priority inversion

### RWLock
- **Reader-preference**: writers podem starve
- **Writer-preference**: readers podem starve
- **Fair**: fila única, ordem FIFO

### Condition Variables
- **Mesa semantics**: `wait` rechecka condição (spurious wakeups)
- **Hoare semantics**: sinal transfere lock diretamente (raro)

### Outras
- **Semaphore**: contador + fila
- **Barrier** (sense-reversing): sincronização de fase
- **CountDownLatch**: espera contagem chegar a zero
- **Phaser**: barreiras flexíveis, fases dinâmicas
- **StampedLock**: optimistic reads (validate stamp), read/write locks

---

## Modelos de Memória

### Hierarquia de Fortaleza
```
SC (Sequential Consistency) ← mais forte
    ↑
x86-TSO (Total Store Order)  ← x86/AMD64
    ↑
C++11/Java/Rust (happens-before, release/acquire, seq_cst, relaxed)
    ↑
ARM/POWER (weak ordering)    ← ARM, POWER, RISC-V
    ↑
RC11 / Promising Semantics   ← formalizações modernas
```

### Modelos Principais

#### Sequential Consistency (Lamport 1979)
- Resultado = alguma intercalação sequencial de operações por thread
- Cada thread vê suas ops em ordem de programa

#### x86-TSO
- **Store Buffer**: writes vão para buffer antes de L1
- **MFENCE**: drena store buffer
- **Lock-prefixed**: atomic RMW (xchg, cmpxchg)

#### C++11 / Java / Rust
- **happens-before**: partial order (program order + synchronizes-with)
- **release/acquire**: store-release + load-acquire = synchronizes-with
- **seq_cst**: total order global (SC para atomics seq_cst)
- **relaxed**: apenas atomicidade, sem ordering

#### ARM/POWER
- **DMB** (Data Memory Barrier): ordering
- **DSB** (Data Synchronization Barrier): completion
- **ISB** (Instruction Synchronization Barrier): pipeline

### Litmus Tests Clássicos
| Teste | SC | TSO | C++11 rel/acq | ARM |
|-------|----|-----|---------------|-----|
| **MP** (Message Passing) | ✓ | ✓ | ✓ | ✗ |
| **SB** (Store Buffering) | ✗ | ✗ | ✗ | ✗ |
| **LB** (Load Buffering) | ✗ | ✓ | ✗ | ✗ |
| **IRIW** (Independent Reads) | ✓ | ✓ | ✗ | ✗ |

---

## Estruturas Lock-Free

### Primitivas Atômicas
- **CAS** (Compare-And-Swap): `bool compare_exchange(expected, desired)`
- **LL/SC** (Load-Linked/Store-Conditional): RISC-V, ARM, PowerPC
- **Problema ABA**: tagged pointers, hazard pointers, epoch-based reclamation

### Estruturas Clássicas
| Estrutura | Paper | Reclamação |
|-----------|-------|------------|
| **Treiber Stack** | 1986 | Hazard Pointers / EBR |
| **Michael-Scott Queue** | 1996 | Hazard Pointers / EBR |
| **Harris List** | 2001 | Hazard Pointers / EBR |
| **Fraser Skip List** | 2003 | Hazard Pointers / EBR |

### Reclamação de Memória
- **Hazard Pointers** (Michael 2004): threads anunciam ponteiros em uso
- **Epoch-Based Reclamation** (Fraser 2004): épocas globais, grace periods
- **QSBR** (Quiescent State-Based Reclamation): RCU-style
- **RCU** (Read-Copy-Update): leitores sem lock, writers copiam

---

## Consenso Distribuído

### FLP Impossibility
- **Resultado**: Consenso determinístico impossível em sistema assíncrono com 1 falha
- **Soluções**: sincronia parcial (timeouts), aleatoriedade, failure detectors

### Paxos
- **Single-Decree**: prepare/promise → accept/accepted
- **Multi-Paxos**: leader estável, log replicado
- **Fast Paxos**: 2 round-trips no caso comum
- **Cheap Paxos**: menos réplicas com auxiliary learners

### Raft (Ongaro & Ousterhout 2014)
- **Leader Election**: termos, vote request, maioria
- **Log Replication**: append entries, commit index, apply
- **Membership Changes**: joint consensus, single-server changes
- **Snapshotting**: log compaction, install snapshot

### Byzantine Fault Tolerance
- **PBFT** (Castro & Liskov 1999): 3f+1 réplicas, 3 fases (pre-prepare, prepare, commit)
- **Tendermint**: BFT + Proof-of-Stake, lock/commit rounds
- **HotStuff**: threshold signatures, linear view change, Chained HotStuff

---

## Actors / Message Passing

### Modelo de Atores (Hewitt 1973, Agha 1986)
- **Tudo é ator**: estado + comportamento + mailbox
- **Mensagens assíncronas**: `send`, `become` (mudança de comportamento)
- **Supervisão**: árvore de falhas (let it crash)

### Erlang/OTP
- **Processos leves**: ~KB stack, milhões possíveis
- **Hot code reload**: upgrade sem downtime
- **Supervisors**: one-for-one, one-for-all, rest-for-one
- **GenServer**: comportamento padrão cliente-servidor

### Akka (JVM/Scala)
- **Typed Actors**: protocolo tipado
- **Cluster Sharding**: distribuição de entities
- **Persistence**: event sourcing, snapshots

### Orleans (Virtual Actors)
- **Grains**: identidade estável, ativação sob demanda
- **Silos**: runtime hosts
- **Streams**: pub/sub integrados

---

## Async/Await

### Stackless vs Stackful
| Tipo | Linguagens | Características |
|------|------------|-----------------|
| **Stackless** | C++20, Rust, C#, Kotlin | State machine, sem stack própria |
| **Stackful** | Go, Lua, Kotlin (coroutines) | Stack própria, blocking natural |

### Work-Stealing Schedulers
- **Cilk**: spawn/sync, work-stealing deque
- **Go**: G-M-P model, netpoller, sysmon
- **Tokio**: multi-threaded, LIFO slot, budget
- **.NET**: ThreadPool, async/await, ValueTask

### I/O Multiplexing
- **epoll** (Linux), **kqueue** (BSD/macOS), **IOCP** (Windows), **io_uring** (Linux 5.1+)
- **Reactor**: demux + dispatch (select/epoll)
- **Proactor**: async I/O + completion (IOCP, io_uring)

### Structured Concurrency
- **Nurseries** (Trio, Kotlin coroutines): escopo de vida, cancelamento propagado
- **Cancellation**: tokens, propagation, cleanup

---

## Verificação Formal

### Model Checking
- **SPIN** (Promela): explicit state, LTL
- **TLC** (TLA+): explicit + symbolic, invariants
- **NuSMV**: symbolic (BDD), CTL/LTL
- **IC3/PDR**: SAT-based, infinite state

### Lógicas Temporais
- **LTL** (Linear Temporal Logic): caminhos lineares, `X, F, G, U`
- **CTL** (Computation Tree Logic): ramificação, `EX, EF, EG, EU`
- **CTL***: unifica LTL + CTL
- **μ-calculus**: fixpoints, expressivo

### Reduções
- **Partial Order Reduction**: explora interleavings representativos
- **Symmetry Reduction**: estados simétricos = 1 representativo

### Lógicas de Programa
- **Separation Logic**: Reynolds, O'Hearn — heap disjunto, frame rule
- **Concurrent Separation Logic**: O'Hearn — CSL, recursos
- **Rely-Guarantee**: Jones — interferência de ambiente
- **Owicki-Gries**: prova de programas concorrentes
- **Iris**: Higher-Order, ghost state, logical relations, invariants

### Ferramentas de Verificação
- **VeriFast**: C/Java, separation logic
- **Dafny**: linguagem + verifier, SMT-backed
- **CBMC**: C bounded model checker
- **F***: dependent types + effects + SMT

---

## Padrões Distribuídos

### Replicação
| Modelo | Consistência | Latência | Disponibilidade |
|--------|--------------|----------|-----------------|
| **Single-Leader** | Strong | Escrita no leader | Leader = SPOF |
| **Multi-Leader** | Eventual | Escrita local | Conflitos |
| **Leaderless/Dynamo** | Eventual/Quorum | Qualquer réplica | Alta |

### Modelos de Consistência
- **Linearizabilidade**: ops aparecem atômicas em tempo real
- **Consistência Sequencial**: ops por processo em ordem, global qualquer
- **Causalidade**: causa antes de efeito
- **Eventual**: converge sem escritas
- **PRAM** (Pipelined RAM): writes de cada processo em ordem

### CRDTs (Conflict-free Replicated Data Types)
| Tipo | Estado | Operação |
|------|--------|----------|
| **G-Counter** | Inteiro | Increment |
| **PN-Counter** | P + N | Inc/Dec |
| **LWW-Register** | (timestamp, value) | Write |
| **OR-Set** | (element, tag) | Add/Remove |
| **RGA** (Replicated Growable Array) | Lista + timestamps | Insert/Delete |

### Transações Distribuídas
- **2PC** (Two-Phase Commit): prepare → commit/abort, bloqueio
- **3PC** (Three-Phase): non-blocking, timeout
- **Saga**: coreografia/orquestração, compensação
- **Calvin/Spanner**: determinismo + Paxos, TrueTime

---

*Próximo: [Fundamentos](../fundamentals/concept.md) | [Paradigmas](../paradigms/concept.md) | [Algoritmos](../algorithms/concept.md) | [Internals de Linguagem](../language-internals/concept.md)*