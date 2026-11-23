# Trilhas de Aprendizado Recomendadas

## Iniciante → Intermediário

### 1. Fundamentos Matemáticos e Computacionais
- `fundamentals/concept.md` + `fundamentals/implementation.md`
- Foque em: lógica proposicional, teoria de conjuntos, lambda calculus básico, complexidade

### 2. Paradigmas de Programação
- `paradigms/concept.md` → escolha **um** paradigma → `paradigms/implementation.md`
- Recomendado: **Funcional** (base para sistemas de tipos, concorrência, verificação)

### 3. Algoritmos Essenciais
- `algorithms/sorting.md`, `algorithms/search.md`, `algorithms/hash_tables.md`, `algorithms/bst.md`
- Implemente cada um do zero em sua linguagem preferida

### 4. Concorrência Básica
- `concurrency/thread_models.md`, `concurrency/sync_primitives.md`
- Escreva: mutex, channel, actor simples

---

## Intermediário → Avançado

### 5. Algoritmos Avançados
- `algorithms/graph_algos.md`, `algorithms/dp.md`, `algorithms/parallel_algorithms.md`
- Resolva problemas competitivos (LeetCode Hard, Codeforces Div1)

### 6. Internals de Linguagem (Pipeline Completo)
- `language-internals/lexer_parser.md` → `type_inference.md` → `ir_optimization.md`
- Construa: lexer → parser → type checker → SSA → otimizador → codegen

### 7. Runtime e GC
- `language-internals/garbage_collection.md` → `runtime_vm.md`
- Implemente: 2-3 algoritmos GC, VM stack-based simples

### 8. Semântica Formal
- `language-internals/formal_semantics.md`
- Prove: type safety (progress + preservation) para STLC

### 9. Concorrência Avançada
- `concurrency/consensus.md`, `concurrency/lockfree_structures.md`
- `concurrency/memory_model.md` + litmus tests
- Implemente: Raft, lock-free queue, verifique com herd7/cat

### 10. Verificação
- `concurrency/verification.md` (planejado), `language-internals/formal_semantics.md` (Iris, Separation Logic)
- Use: Coq/Lean/Agda/Dafny para provar propriedades de programas concorrentes

---

## Avançado → Expert

### 11. Fase 7 (Planejada): Domínios Especializados
- **Systems**: OS kernels, filesystems, networking stack, eBPF
- **Graphics**: Rendering pipeline, GPU compute, Vulkan/Metal/DX12
- **Cryptography**: Primitivas, protocolos, zero-knowledge, post-quantum
- **ML Systems**: Training systems, inference serving, feature stores, MLOps
- **Formal Methods**: Coq/Lean/Isabelle, TLA+, model checking, theorem proving

### 12. Fase 8 (Planejada): Fronteira 2024-2026+
- **AI-Assisted Coding**: Copilot, Cursor, agent-based development
- **WebAssembly**: Components, WASI, component model, plugins
- **Effect Systems**: Koka, Eff, algebraic effects, handlers
- **Quantum Programming**: Q#, Cirq, error correction, NISQ algorithms
- **Novas Linguagens**: Rust, Zig, Carbon, Vale, Mojo, MoonBit

### 13. Fase 9 (Planejada): Síntese para Treinamento de IA
- **Curriculum Design**: Spiral learning, prerequisite graphs
- **Exercise Generation**: Procedural, difficulty calibration
- **Evaluation Framework**: Rubrics, automated grading, progress tracking
- **Knowledge Distillation**: From expert to student model
- **Interactive Teaching**: Socratic dialogue, worked examples, fading

---

## Projetos Capstone por Nível

| Nível | Projeto | Habilidades Exercitadas |
|-------|---------|------------------------|
| **Iniciante** | Calculadora RPN + parser | Lexer, parser, stack, recursão |
| **Iniciante** | Mini Redis (in-memory) | Hash table, protocol parsing, concorrência básica |
| **Intermediário** | Compilador STLC → bytecode + VM | Pipeline completo, type checking, codegen |
| **Intermediário** | Raft implementation | Consenso, logs, snapshots, membership changes |
| **Avançado** | Verified concurrent queue (Iris/Coq) | Separation logic, ghost state, linearizability |
| **Avançado** | Incremental compiler com Salsa/Inc | Query-based, incremental, caching |
| **Expert** | Research contribution | Nova otimização, novo algoritmo, formalização |

---

## Recursos Complementares

### Livros Essenciais
| Área | Livro |
|------|-------|
| Algoritmos | CLRS (Cormen et al.), DPV (Dasgupta/Papadimitriou/Vazirani) |
| Compiladores | Dragon Book (Aho et al.), Engineering a Compiler (Cooper/Torczon) |
| Tipos | TAPL (Pierce), PFPL (Harper) |
| Concorrência | Art of Multiprocessor Programming (Herlihy/Shavit) |
| Distribuídos | DDIA (Kleppmann), Distributed Systems (Coulouris et al.) |
| Verificação | Software Foundations (Pierce et al.), Concrete Semantics (Nipkow/Klein) |

### Cursos Online
- **MIT 6.004** (Computation Structures)
- **MIT 6.824** (Distributed Systems)
- **CMU 15-411** (Compiler Design)
- **Stanford CS243** (Program Analysis)
- **UW CSE 505** (Programming Languages)

### Ferramentas de Prática
- **Compiler Explorer** (godbolt.org) — assembly, IR
- **Herd7 / cat** — litmus tests memory models
- **TLA+ Toolbox** — model checking specs
- **Coq / Lean / Agda / Isabelle** — theorem proving
- **Dafny / F* / VeriFast** — verification-oriented languages

---

## Métricas de Progresso

| Marco | Critério |
|-------|----------|
| **Iniciante → Intermediário** | Implementa 10+ estruturas/algoritmos do zero, explica trade-offs |
| **Intermediário → Avançado** | Escreve compilador funcional, GC, ou sistema distribuído correto |
| **Avançado → Expert** | Contribui para pesquisa (paper, tool, formalização), ensina outros |

---

*Próximo: [Princípios de Desenvolvimento](../about/principles.md) | [Workflow de Skills](workflow.md)*