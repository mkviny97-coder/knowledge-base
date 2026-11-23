# Internals de Linguagem — Compiladores, Runtime, GC, Type Systems

## Visão Geral

Pipeline completo de compilador: frontend (lexer, parser, semantic analysis), middle-end (IR, otimizações), backend (codegen, runtime). Inclui 9 algoritmos GC, VMs, JIT, semântica formal.

---

## Frontend: Lexical Analysis & Parsing

### Análise Léxica
- **Expressões Regulares → DFA**: Thompson NFA → Subset Construction → DFA minimizado (Hopcroft)
- **Unicode**: categorias (Letter, Number, Mark, Symbol, Punctuation, Separator, Other)
- **Tokenização**: maximal munch, keywords vs identifiers, raw strings, interpolation

### Parsing
| Algoritmo | Gramática | Complexidade | Uso |
|-----------|-----------|--------------|-----|
| **LL(k)** | LL(k) | O(n) | Parsers recursivos, ANTLR |
| **LR(1)** | LR(1) | O(n) | yacc, bison, menhir |
| **LALR(1)** | LALR(1) | O(n) | yacc/bison default |
| **GLR** | CFG ambígua | O(n³) worst | Elkhound, Bison GLR |
| **PEG** | Parsing Expression Grammar | O(n) packrat | Rats!, peg.js |
| **Pratt** | Precedence climbing | O(n) | TypeScript, Rust, Lua |

### Recuperação de Erros
- **Panic mode**: sincroniza em tokens de sincronização (;, }, end)
- **Error productions**: regras para erros comuns
- **Minimum-distance repair**: A* sobre edições (insert/delete/replace)

### AST Design
- **Typed nodes**: cada nó carrega tipo (pós-semantic analysis)
- **Visitor pattern**: separa travessia de operação
- **Source locations**: span (start, end) para mensagens de erro

---

## Sistemas de Tipos

### Hierarquia de Expressividade
```
STLC → System F → System Fω → CoC → Dependent Types (MLTT)
      ↑                    ↑
   Polimorfismo        Operadores
   paramétrico         de tipo
```

### Hindley-Milner (Algorithm W)
- **Let-polymorphism**: generalização apenas em `let` (value restriction)
- **Unificação**: Robinson com occurs-check
- **Principal types**: tipo mais geral (principal typing property)
- **Extensões**: type classes (Haskell), traits (Rust), implicits (Scala)

### Bidirectional Type Checking
- **Check mode**: `Γ ⊢ e ⇐ τ` (termo tem tipo esperado)
- **Synth mode**: `Γ ⊢ e ⇒ τ` (termo sintetiza tipo)
- **Vantagens**: decidível para tipos dependentes, melhores erros

### Tipos Dependentes
- **Π-types**: `(x : A) → B x` (função dependente)
- **Σ-types**: `(x : A) × B x` (par dependente)
- **Tipos Indutivos**: `data Nat = Zero | Succ Nat`
- **Eliminadores**: pattern matching, recursão estrutural
- **Universos**: `Type₀ : Type₁ : Type₂ ...` (evita paradoxos)

### Tipos Lineares / Afinés / Efeitos
- **Linear**: usado exatamente 1x (Rust ownership, Clean)
- **Afiné**: usado ≤ 1x (descarta permitido)
- **Efeitos Algébricos**: `effect State { get : Unit → Int; put : Int → Unit }`
- **Handlers**: `handle e with { get → λ_. put 42; ... }`
- **Row Polymorphism**: extensibilidade de efeitos/records

### Gradual Typing
- **Consistência**: `τ ~ ?` (dynamic type)
- **Blame Calculus**: rastreia cast failures para módulo culpado
- **Exemplos**: TypeScript, Racket, Typed Racket, Pyret

---

## Middle-End: IR e Otimizações

### SSA (Static Single Assignment)
- **Construção Cytron et al.**: dominadores (Lengauer-Tarjan), frontier de dominância
- **φ-functions**: merge de definições em pontos de junção
- **Pruned SSA**: apenas variáveis vivas
- **SSA deconversion**: register allocation, copy coalescing

### Dataflow Analysis
- **Lattice Theory**: partial order, meet/join, top/bottom, altura finita
- **Monotone Framework**: transfer functions, worklist algorithm (chaotic iteration)
- **Análises Clássicas**:
  - **Reaching Definitions**: forward, may
  - **Live Variables**: backward, may
  - **Available Expressions**: forward, must
  - **Very Busy Expressions**: backward, must

### Otimizações Clássicas
| Otimização | Descrição |
|------------|-----------|
| **GVN** (Global Value Numbering) | Particiona valores em classes de equivalência |
| **LICM** (Loop Invariant Code Motion) | Move computação invariante para preheader |
| **PRE** (Partial Redundancy Elimination) | Unifica CSE + LICM + code hoisting |
| **DCE** (Dead Code Elimination) | Remove código inalcançável / sem efeito |
| **CP** (Constant Propagation) | Propaga constantes, fold |
| **CSE** (Common Subexpression Elimination) | Reusa computações idênticas |

### Otimizações de Loop
- **Invariant Code Motion**: LICM
- **Unswitching**: move condição invariante fora do loop
- **Fusion**: combina loops adjacentes (melhora localidade)
- **Fission**: divide loop (permite paralalelismo)
- **Tiling/Blocking**: melhora cache (matrix multiply)
- **Vectorization**: SLP (superword), loop vectorization
- **Polyhedral Model**: Pluto, ISL — transformações afins

### Otimizações Interprocedurais
- **IPA**: call graph, points-to, escape analysis
- **Devirtualization**: resolve chamadas virtuais
- **Inlining**: heurísticas (tamanho, frequência, hotness)
- **PGO** (Profile-Guided Optimization): feedback-directed
- **LTO** (Link-Time Optimization): whole-program no link

### Otimizações Especulativas
- **Guard Insertion**: check + fast path + slow path (deopt)
- **Deoptimization / OSR**: volta para interpreter, recompila
- **Inline Caching**: monomorphic → polymorphic PIC → megamorphic

---

## Backend: Codegen e Runtime

### IRs Principais
| IR | Linguagem/Projeto | Características |
|----|-------------------|-----------------|
| **LLVM IR** | LLVM, Clang, Rust, Swift | SSA, typed, target-independent |
| **MLIR** | LLVM, TensorFlow, IREE | Multi-level, dialects, extensível |
| **WebAssembly** | Wasm, wasmtime, wasmer | Stack machine, sandboxed, portable |
| **GHC Core** | GHC Haskell | System FC, typed, explícito |
| **Rust MIR** | rustc | Control-flow graph, borrowck, desugared |

### Calling Conventions
- **System V AMD64**: RDI, RSI, RDX, RCX, R8, R9 (args), RAX/RDX (ret)
- **Windows x64**: RCX, RDX, R8, R9 (args), stack shadow space
- **ARM64 AAPCS**: X0-X7 (args), X0/X1 (ret), FP/LR

### Frame Management
- **Stack frames**: base pointer (RBP) ou frame pointer omission
- **Stack unwinding**: DWARF (ELF), SEH (Windows), .eh_frame
- **Exception Handling**: Itanium ABI (personality routine, LSDA), SEH

### JIT Compilation
| Tipo | Descrição | Exemplos |
|------|-----------|----------|
| **Tracing JIT** | Grava trace quente, compila | LuaJIT, PyPy, V8 (Ignition+TurboFan) |
| **Method JIT** | Compila método por método | JVM (C1/C2), .NET (RyuJIT), GraalVM |
| **Tiered Compilation** | Interpreter → baseline JIT → optimizing JIT | V8, SpiderMonkey, JVM |
| **AOT** | Ahead-of-time | GraalVM Native Image, .NET Native, Rust |

### Inline Caching
- **Monomorphic**: single target, direct call
- **Polymorphic (PIC)**: few targets, linear search / jump table
- **Megamorphic**: many targets, hash table / call site cache

---

## Gerenciamento de Memória: 9 Algoritmos GC

| Algoritmo | Tipo | Pausa | Throughput | Uso |
|-----------|------|-------|------------|-----|
| **RefCount** | Contagem | Baixa | Baixo (ciclos) | Python, Swift, COM |
| **Mark-Sweep** | Tracing | Média | Médio | Lua, Boehm GC |
| **Mark-Compact** | Tracing + Move | Alta | Médio | JVM (CMS antigo) |
| **Copying (Cheney)** | Tracing + Move | Baixa | Alto | JVM (nursery), Go |
| **Generational** | Híbrido | Baixa (minor) | Alto | JVM (G1, ZGC), .NET, V8, Go |
| **Incremental** | Fatiado | Muito baixa | Menor | Real-time systems |
| **Concurrent** | Paralelo | Mínima | Alto | JVM (ZGC, Shenandoah), Go |
| **ZGC** | Colored pointers | <1ms | Alto | JDK 11+ (heap multi-TB) |
| **Shenandoah** | Brooks pointers | <10ms | Alto | JDK 12+, Red Hat |
| **Region-Based** | TTL/Regiões | Previsível | Variável | Rust (drop), Cyclone, Tofte-Talpin |

### Alocadores
- **Bump Pointer**: nursery, fast-path
- **Free List**: size classes, fragmentation
- **TLAB** (Thread-Local Allocation Buffer): sem contention
- **Large Object**: direct mmap, bypass nursery

---

## VMs e Máquinas Abstratas

### Stack VM (JVM-style)
- **Operand stack**: push/pop, aritmética, chamadas
- **Local variables**: array indexado
- **Bytecode**: verificação (stack map frames), segurança

### Register VM (Lua 5.0+, Dalvik, LuaJIT)
- **Registradores virtuais**: instruções 3-address
- **Menos instruções**: ~30% menos que stack VM
- **SSA-friendly**: mapeamento direto

### JIT + OSR + Deopt
- **OSR** (On-Stack Replacement): entrada no meio de loop compilado
- **Deoptimization**: recompilação, state reconstruction
- **Speculation guards**: type checks, null checks, range checks

---

## Semântica Formal

### Semântica Operacional
- **SOS Small-Step**: `e → e'` (um passo), regras de redução
- **Big-Step / Natural**: `e ⇓ v` (avaliação completa)
- **Máquinas Abstratas**:
  - **CEK**: Control, Environment, Continuation
  - **SECD**: Stack, Environment, Control, Dump
  - **Krivine**: weak head reduction, call-by-name
  - **ZAM**: Zinc Abstract Machine (OCaml bytecode)
  - **CAM**: Categorical Abstract Machine

### Semântica Axiomática
- **Hoare Logic**: `{P} c {Q}`, regras de atribuição, sequenciação, loop
- **Separation Logic**: `P * Q` (heap disjunto), frame rule
- **Refinement Types / Liquid Types**: `{v:T | p(v)}`, SMT-backed
- **Iris**: Higher-Order Concurrent Separation Logic, ghost state, logical relations

### VCG (Verification Condition Generator)
- Gera VCs de programa anotado → SMT solver (Z3, CVC5)
- **Dafny**, **F***, **VeriFast**, **Why3**

---

*Próximo: [Fundamentos](../fundamentals/concept.md) | [Paradigmas](../paradigms/concept.md) | [Algoritmos](../algorithms/concept.md) | [Concorrência](../concurrency/concept.md)*