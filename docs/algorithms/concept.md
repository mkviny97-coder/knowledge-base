# Estruturas de Dados e Algoritmos — Core + Avançado

## Visão Geral

Esta fase cobre 25+ tópicos algorítmicos: desde fundamentos (sorting, search, grafos) até avançados (paralelos, streaming, quânticos, aproximação, cache-oblivious, persistentes).

---

## Complexidade e Análise

### Notação Assintótica
- **O (Big-O)**: limite superior assintótico
- **Ω (Big-Omega)**: limite inferior
- **Θ (Theta)**: limite exato (O ∩ Ω)
- **o (little-o)**: estritamente menor
- **ω (little-omega)**: estritamente maior

### Análise Amortizada
- **Método Agregado**: custo total / n operações
- **Método do Potencial**: Φ(D) função de potencial, custo amortizado = custo real + ΔΦ
- **Método Contábil**: créditos pré-pagos

### Classes de Complexidade
```
L ⊆ NL ⊆ P ⊆ NP ⊆ PH ⊆ PSPACE ⊆ EXP ⊆ NEXP ⊆ EXPSPACE
```
- **P**: tempo polinomial determinístico
- **NP**: tempo polinomial não-determinístico (certificados verificáveis em P)
- **NP-completo**: NP + todo NP reduz a ele (Cook-Levin: SAT)
- **PH**: hierarquia polinomial (Σᵢ^P, Πᵢ^P)
- **PSPACE**: espaço polinomial = NPSPACE (Savitch)
- **BQP**: tempo polinomial quântico com erro limitado

---

## Estruturas de Dados Fundamentais

### Arrays e Listas
- **Array**: acesso O(1), inserção/deleção O(n)
- **Linked List**: inserção/deleção O(1) com ponteiro, acesso O(n)
- **Gap Buffer / Rope**: edição de texto eficiente

### Hash Tables
- **Endereçamento aberto**: linear probing, quadratic, double hashing, **Robin Hood**
- **Encadeamento**: listas, árvores (Java 8+), **consistent hashing** (distribuído)
- **Cuckoo Hashing**: O(1) worst-case lookup, duas funções hash
- **Perfect Hashing**: estático, O(1) garantido (FKS)

### Árvores Balanceadas
| Árvore | Inserção | Busca | Deleção | Caso de Uso |
|--------|----------|-------|---------|-------------|
| **AVL** | O(log n) | O(log n) | O(log n) | Busca frequente, pouca escrita |
| **Red-Black** | O(log n) | O(log n) | O(log n) | Uso geral (std::map, TreeMap) |
| **B-Tree / B+Tree** | O(logₐ n) | O(logₐ n) | O(logₐ n) | Disco, bancos de dados |
| **Splay** | O(log n)* | O(log n)* | O(log n)* | Localidade temporal |
| **Treap** | O(log n) | O(log n) | O(log n) | Aleatorizada, simples |

*amortizado

### Heaps
- **Binary Heap**: array, O(log n) insert/extract, O(n) build
- **Fibonacci Heap**: O(1) insert/merge, O(log n) extract, decrease-key O(1)*
- **Pairing Heap**: simples, bom na prática
- **Binomial Heap**: merge O(log n), base para Fibonacci
- **Leftist Heap**: merge O(log n), variant skew heap

### Union-Find (Disjoint Set Union)
- **Path Compression**: achata caminho no find
- **Union by Rank/Size**: anexa menor ao maior
- **Complexidade**: O(α(n)) ≈ O(1) amortizado
- **Aplicações**: Kruskal, componentes conectados, offline LCA

---

## Algoritmos de Grafo

### Caminhos Mínimos
| Algoritmo | Complexidade | Restrição |
|-----------|-------------|-----------|
| **Dijkstra** | O((V+E) log V) | Pesos ≥ 0 |
| **A*** | O((V+E) log V) | Heurística admissível |
| **Bellman-Ford** | O(VE) | Pesos negativos, detecta ciclo negativo |
| **Floyd-Warshall** | O(V³) | Todos-pares, pesos negativos (sem ciclo) |
| **Johnson** | O(VE + V² log V) | Todos-pares, esparso |

### Fluxo Máximo
- **Dinic**: O(E√V) bipartido, O(V²E) geral
- **Push-Relabel**: O(V²√E) com gap heuristic
- **Gomory-Hu Tree**: todos-pares min-cut em O(V) max-flows

### Matching
- **Hopcroft-Karp**: O(E√V) bipartido máximo
- **Blossom (Edmonds)**: O(V³) geral, Micali-Vazirani O(√V E)

### MST
- **Kruskal**: O(E log E) + DSU
- **Prim**: O(E log V) com heap
- **Boruvka**: O(E log V), paralelo

---

## Algoritmos Avançados

### Programação Dinâmica
- **Padrões**: Knapsack, LCS, Edit Distance, Matrix Chain, Optimal BST
- **Otimizações**:
  - **Knuth**: quadrangle inequality → O(n²) → O(n²) com constante menor
  - **Divide & Conquer DP**: monotonicidade de decisões → O(n log n)
  - **Convex Hull Trick**: linhas convexas → O(log n) por transição
  - **Aliens Trick**: Lagrangian relaxation para cardinality constraints

### Algoritmos Gulosos
- **Matróides**: estrutura de independência → guloso ótimo
- **Interval Scheduling**: earliest finish time
- **Huffman Coding**: árvore de prefixo ótima
- **Kruskal/Prim**: MST via troca de corte

### Dividir e Conquistar
- **FFT (Cooley-Tukey)**: O(n log n) multiplicação polinomial, convolução
- **Strassen**: O(n^log₂₇) ≈ O(n²·⁸¹) multiplicação de matrizes
- **Karatsuba**: O(n^log₂₃) ≈ O(n¹·⁵⁸) multiplicação inteira
- **Closest Pair**: O(n log n) plano

### Backtracking / SAT
- **Constraint Satisfaction**: forward checking, arc consistency
- **CDCL SAT Solvers**: VSIDS, clause learning, restarts, phase saving
- **N-Queens**: bitmasks + simetria

### Algoritmos Aleatorizados
- **Monte Carlo**: pode errar (ex: primalidade Miller-Rabin)
- **Las Vegas**: sempre correto, tempo aleatório (ex: QuickSelect)
- **QuickSelect**: O(n) esperado, mediana das medianas O(n) worst-case
- **Skip Lists**: O(log n) esperado, alternativa a árvores balanceadas

### Algoritmos de Aproximação
- **PTAS**: (1+ε)-aproximação em tempo polinomial para ε fixo
- **FPTAS**: PTAS + tempo polinomial em 1/ε
- **LP Rounding**: relaxação linear + arredondamento
- **Primal-Dual**: construído via dual do LP
- **Set Cover**: guloso ln n-aproximação
- **TSP Métrico**: Christofides 1.5-aproximação

---

## Estruturas Avançadas

### Persistentes (Imutáveis)
- **Path Copying**: O(log n) espaço/tempo por atualização
- **Fat Nodes**: O(1) espaço extra, O(log n) tempo com versionamento
- **Persistent Segment Tree**: O(log n) por versão
- **Persistent DSU**: O(log n) com rollback (undo)

### Cache-Oblivious
- **Ideal Cache Model**: cache de tamanho Z, linha B, ótimo off-line
- **Van Emde Boas Layout**: árvores em ordem Z para localidade
- **Cache-Oblivious B-Tree**: O(logₐ N) I/Os
- **Matrix Multiply**: recursivo, O(n³ / (B√Z)) I/Os

### Probabilísticas
- **Bloom Filter**: O(k) bits, falso positivo, sem falso negativo
- **Count-Min Sketch**: frequências aproximadas, O(1/ε log 1/δ)
- **HyperLogLog**: cardinalidade distinta, O(log log n) bits
- **Reservoir Sampling**: amostra uniforme de stream tamanho desconhecido

### Paralelos / Streaming
- **Work-Stealing** (Cilk, Go, Tokio): deque por worker, steal do topo
- **PRAM**: EREW, CREW, CRCW — modelo teórico
- **Parallel Prefix (Scan)**: Blelloch, Hillis-Steele
- **MapReduce Patterns**: map → shuffle → reduce
- **Sliding Window**: agregações em janela temporal
- **Distributed Consensus**: Raft, Paxos

### Quânticos
- **Grover**: O(√N) busca não-estruturada
- **Shor**: O((log N)³) fatoração, log discreto
- **QFT**: transformada de Fourier quântica
- **VQE/QAOA**: variacional, NISQ
- **Error Correction**: surface codes, stabilizer codes

---

## Guia de Implementação por Linguagem

| Estrutura | Python | Rust | C++ | Go | Java |
|-----------|--------|------|-----|-----|------|
| Hash Table | `dict` | `HashMap` | `unordered_map` | `map` | `HashMap` |
| TreeMap | `sortedcontainers` | `BTreeMap` | `map` | - | `TreeMap` |
| Heap | `heapq` | `BinaryHeap` | `priority_queue` | `container/heap` | `PriorityQueue` |
| DSU | custom | custom | custom | custom | custom |
| Graph | `networkx` | `petgraph` | `boost::graph` | custom | `JGraphT` |

---

*Próximo: [Fundamentos](../fundamentals/concept.md) | [Paradigmas](../paradigms/concept.md) | [Internals de Linguagem](../language-internals/concept.md) | [Concorrência](../concurrency/concept.md)*