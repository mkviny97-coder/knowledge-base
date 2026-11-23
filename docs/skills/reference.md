# Guia de Referência Rápida: Qual Arquivo Ler Para Cada Necessidade

## Tabela Principal

| NECESSIDADE | ARQUIVO PRINCIPAL |
|-------------|-------------------|
| Entender gerenciamento de memória (GC) | `language-internals/garbage_collection.md` |
| Construir parser/lexer | `language-internals/lexer_parser.md` |
| Implementar type inference (HM, bidirectional) | `language-internals/type_inference.md` |
| Otimizar IR de compilador (SSA, dataflow) | `language-internals/ir_optimization.md` |
| Construir VM/JIT/Interpreter | `language-internals/runtime_vm.md` |
| Provar correção de programas | `language-internals/formal_semantics.md` |
| Escolher modelo de threads | `concurrency/thread_models.md` |
| Implementar sincronização (mutex, RWLock, etc) | `concurrency/sync_primitives.md` |
| Entender memory ordering (SC, TSO, C++11) | `concurrency/memory_model.md` |
| Construir estruturas lock-free | `concurrency/lockfree_structures.md` |
| Implementar consenso (Paxos, Raft, PBFT) | `concurrency/consensus.md` |
| Aprender qualquer algoritmo | `algorithms/<tópico>.md` |
| Escolher paradigma de programação | `paradigms/concept.md` |
| Refrescar fundamentos matemáticos | `fundamentals/concept.md` |
| Verificar propriedades temporais | `concurrency/temporal_logic.md` (planejado) |
| Model checking de sistemas concorrentes | `concurrency/model_checker.md` (planejado) |
| CRDTs para dados distribuídos | `concurrency/crdt.md` (planejado) |
| Transações distribuídas (2PC, Saga) | `concurrency/distributed_tx.md` (planejado) |
| Actor runtime com supervisão | `concurrency/actor_runtime.md` (planejado) |
| Async runtime com io_uring | `concurrency/async_runtime.md` (planejado) |

---

## Algoritmos — Arquivos por Tópico

| Tópico | Arquivo |
|--------|---------|
| Pilhas, filas, deques, filas circulares | `algorithms/stacks_queues.md` |
| Hash tables, consistent hashing, robin hood | `algorithms/hash_tables.md` |
| AVL, Red-Black, B-tree, Splay, Treap | `algorithms/bst.md` |
| Binary, Fibonacci, Pairing, Binomial, Leftist | `algorithms/heaps.md` |
| DSU com path compression, union by rank | `algorithms/union_find.md` |
| Range queries, lazy propagation, persistent | `algorithms/segment_tree.md` |
| Prefix trees, Radix, Suffix trees, Aho-Corasick | `algorithms/tries.md` |
| KMP, Z-algorithm, Suffix Array, Manacher | `algorithms/string_algos.md` |
| Quick, Merge, Heap, Timsort, Introsort, Radix, Counting | `algorithms/sorting.md` |
| Binary, Exponential, Interpolation, Fractional Cascading | `algorithms/search.md` |
| Dijkstra, A*, Bellman-Ford, Floyd-Warshall, Max Flow, MST | `algorithms/graph_algos.md` |
| DP patterns, Knuth optimization, Divide & Conquer DP | `algorithms/dp.md` |
| Matroids, Interval scheduling, Huffman, Kruskal | `algorithms/greedy.md` |
| FFT, Strassen, Closest pair, Karatsuba | `algorithms/divide_conquer.md` |
| Constraint satisfaction, SAT solving, N-Queens | `algorithms/backtracking.md` |
| Monte Carlo, Las Vegas, QuickSelect, Skip lists | `algorithms/randomized.md` |
| PTAS, LP rounding, Set cover, TSP approximations | `algorithms/approximation.md` |
| Classes de complexidade, reduções, hierarquias | `algorithms/complexity.md` |
| Persistent arrays, trees, queues, DSU | `algorithms/persistent.md` |
| Cache-oblivious algorithms, B-trees, matrix multiply | `algorithms/cache_oblivious.md` |
| Work-stealing, PRAM, parallel prefix, sorting | `algorithms/parallel_algorithms.md` |
| Count-Min Sketch, HyperLogLog, Reservoir sampling | `algorithms/streaming_algorithms.md` |
| Grover, Shor, QFT, VQE, Quantum phase estimation | `algorithms/quantum_algorithms.md` |

---

## Internals de Linguagem — Arquivos por Tópico

| Tópico | Arquivo |
|--------|---------|
| Pipeline completo: frontend, middle, backend | `language-internals/concept.md` |
| Lexer (DFA/NFA), Parser (Pratt, Recursive Descent), AST, Error Recovery | `language-internals/lexer_parser.md` |
| Hindley-Milner (Algorithm W), Bidirectional, Constraint solving, Let-polymorphism | `language-internals/type_inference.md` |
| SSA (Cytron et al.), Dataflow (Lattice theory), GVN, LICM, PRE, DCE | `language-internals/ir_optimization.md` |
| 9 algoritmos GC + allocators (2200+ linhas) | `language-internals/garbage_collection.md` |
| Stack VM, Register VM, JIT, OSR, Inline Caching | `language-internals/runtime_vm.md` |
| SOS, Abstract machines (CEK, SECD, Krivine, ZAM), Separation Logic, Iris | `language-internals/formal_semantics.md` |

---

## Concorrência — Arquivos por Tópico

| Tópico | Arquivo |
|--------|---------|
| 1:1, M:1, M:N (Go-style work-stealing) | `concurrency/thread_models.md` |
| Spinlocks (TTAS, Ticket, MCS), Mutex (futex), RWLock, CondVar, Semaphore, Barrier | `concurrency/sync_primitives.md` |
| SC, x86-TSO, ARM/POWER, C++11/Java/Rust (happens-before), Litmus tests | `concurrency/memory_model.md` |
| Treiber Stack, Michael-Scott Queue, Harris List, Skip List, Hazard Pointers, EBR, RCU | `concurrency/lockfree_structures.md` |
| Paxos, Raft, PBFT, Network simulator | `concurrency/consensus.md` |
| Actor model, supervision, location transparency | `concurrency/actor_runtime.md` (planejado) |
| Stackless coroutines, work-stealing, io_uring | `concurrency/async_runtime.md` (planejado) |
| State-based (CvRRT), Operation-based (CmRDT) | `concurrency/crdt.md` (planejado) |
| 2PC, 3PC, Saga pattern | `concurrency/distributed_tx.md` (planejado) |
| Explicit state model checker (Promela-like) | `concurrency/model_checker.md` (planejado) |
| LTL/CTL model checking algorithms | `concurrency/temporal_logic.md` (planejado) |
| Separation logic, Rely-Guarantee, Owicki-Gries, Iris | `concurrency/verification.md` (planejado) |
| Queueing theory, Amdahl/Gustafson/USL calculators | `concurrency/scalability.md` (planejado) |

---

## Fundamentos — Arquivos por Tópico

| Tópico | Arquivo |
|--------|---------|
| Lógica, conjuntos, funções, categorias, teoria de tipos | `fundamentals/concept.md` |
| Implementações de referência | `fundamentals/implementation.md` |
| Trade-offs de design | `fundamentals/tradeoffs.md` |
| Fronteiras de pesquisa atuais | `fundamentals/frontiers.md` |
| Exercícios práticos | `fundamentals/exercises.md` |

---

## Paradigmas — Arquivos por Tópico

| Tópico | Arquivo |
|--------|---------|
| Imperativo, OO, Funcional, Lógico, Concorrente, Metaprogramação | `paradigms/concept.md` |
| Implementações por paradigma | `paradigms/implementation.md` |
| Quando usar cada paradigma | `paradigms/tradeoffs.md` |
| Paradigmas emergentes | `paradigms/frontiers.md` |
| Exercícios | `paradigms/exercises.md` |

---

## Navegação Rápida por Fase

### Fase 1: Fundamentos
```
fundamentals/
├── concept.md          # Teoria base
├── implementation.md   # Código de referência
├── tradeoffs.md        # Decisões de design
├── frontiers.md        # Pesquisa atual
├── exercises.md        # Prática
└── references.bib      # Bibliografia
```

### Fase 2: Paradigmas
```
paradigms/
├── concept.md          # Taxonomia completa
├── implementation.md   # Exemplos por paradigma
├── tradeoffs.md        # Critérios de escolha
├── frontiers.md        # Paradigmas emergentes
└── exercises.md
```

### Fase 3: Algoritmos (25+ arquivos)
```
algorithms/
├── concept.md          # Visão geral + complexidade
├── implementation.md   # Guia de implementação
├── stacks_queues.md
├── hash_tables.md
├── bst.md
├── heaps.md
├── union_find.md
├── segment_tree.md
├── tries.md
├── string_algos.md
├── sorting.md
├── search.md
├── graph_algos.md
├── dp.md
├── greedy.md
├── divide_conquer.md
├── backtracking.md
├── randomized.md
├── approximation.md
├── complexity.md
├── persistent.md
├── cache_oblivious.md
├── parallel_algorithms.md
├── streaming_algorithms.md
├── quantum_algorithms.md
├── tradeoffs.md
├── frontiers.md
├── exercises.md
└── references.bib
```

### Fase 4: Internals de Linguagem
```
language-internals/
├── concept.md          # Pipeline completo
├── lexer_parser.md
├── type_inference.md
├── ir_optimization.md
├── garbage_collection.md
├── runtime_vm.md
├── formal_semantics.md
└── references.bib
```

### Fase 5: Concorrência
```
concurrency/
├── concept.md          # Visão geral completa
├── thread_models.md
├── sync_primitives.md
├── memory_model.md
├── lockfree_structures.md
├── consensus.md
├── actor_runtime.md    (planejado)
├── async_runtime.md    (planejado)
├── crdt.md             (planejado)
├── distributed_tx.md   (planejado)
├── model_checker.md    (planejado)
├── temporal_logic.md   (planejado)
├── verification.md     (planejado)
├── scalability.md      (planejado)
└── references.bib
```

---

*Próximo: [Trilhas de Aprendizado](learning_paths.md) | [Workflow de Skills](workflow.md)*