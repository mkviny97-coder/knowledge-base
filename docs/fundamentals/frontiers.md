# Fronteiras de Pesquisa — Fundamentos

## Lógica e Verificação

### Proof Repair / Auto-formalization
- **LLMs para formalização**: Tradução linguagem natural → Lean/Coq/Isabelle (ex: Lean 4 + GPT-4, miniF2F benchmark)
- **Reparo de provas**: Sugestão de táticas, síntese de `have` statements, `sorry` filling
- **Ferramentas**: Lean 4 `have` tactics, Coq `Ltac2`, Isabelle `Sledgehammer` + ML

### Homomorphic Encryption para Verificação
- Verificação de provas em dados criptografados (privacidade em teoremas)
- Aplicações: verificação de contratos confidenciais, auditoria zero-knowledge

---

## Teoria de Categorias Aplicada

### Categorias ∞-Topos / HoTT (Homotopy Type Theory)
- **Univalência**: Isomorfismo = Igualdade
- **Higher Inductive Types**: Tipos com construtores de caminho (ex: `S¹`, truncamentos)
- **Cubical Type Theory**: Computacional, decidível (Cubical Agda, Redtt)
- **Aplicação**: Formalização de matemática moderna (esquemas, cohomologia)

### Categorias Enriched / Actegories
- **Enriched categories**: Hom-objects em categoria monóide (ex: métricas, probabilidades)
- **Actegories**: Ações de categoria monóide (lentes, ópticas, gradientes)
- **Uso**: Diferenciação automática, programação probabilística, ópticas bidirecionais

---

## Teoria de Tipos

### Dependent Types Ergonomics
- **Elaboração bidirecional** (check/synth) com metavariáveis
- **Implicit arguments** com resolução de type classes (Rust traits, Haskell typeclasses, Lean typeclasses)
- **Pattern matching** em tipos dependentes (Coq `Equations`, Agda `with`, Lean `match`)

### Linear/Quantitative Types
- **Linear Types** (Rust ownership, Clean, Linear Haskell): Recursos usados exatamente uma vez
- **Quantitative Types** (Granule, CoqEAL): Rastreamento de uso (0, 1, ω)
- **Aplicação**: Protocolos de sessão, gerenciamento de memória, privacidade diferencial

### Effect Systems / Algebraic Effects
- **Efeitos algébricos** (Koka, Eff, Frank, Multicore OCaml): Handlers composíveis
- **Row polymorphism** para efeitos: extensibilidade, modularidade
- **Gradual Effect Types**: Mistura tipado/untyped com blame calculus

---

## Complexidade e Computação

### Fine-Grained Complexity
- **Hipótese SETH** (Strong Exponential Time): k-SAT requer 2⁽¹⁻ᵒ⁽¹⁾⁾ⁿ
- **Reduções condicionais**: OVH, 3SUM, APSP equivalências
- **Ferramentas**: `fine-grained` crate, benchmarks condicionais

### Quantum Complexity Prática
- **NISQ algorithms**: VQE, QAOA, quantum approximate optimization
- **Error mitigation**: Zero-noise extrapolation, probabilistic error cancellation
- **Frameworks**: Qiskit, Cirq, PennyLane, CUDA Quantum

### Computação Reversível / Adiabática
- **Landauer limit**: kT ln 2 por bit apagado
- **Linguagens reversíveis**: Janus, R, Theseus
- **Aplicação**: Computação de ultra-baixa energia, criptografia

---

## Síntese de Programas

### Program Synthesis / Inductive Synthesis
- **Syntax-guided synthesis (SyGuS)**: Gramática + especificação → programa
- **Neural-guided search**: LLMs + symbolic search (ex: AlphaCode, Codex)
- **Benchmarks**: ARC, HumanEval, MBPP, SyGuS-Comp

### Deductive Synthesis
- **Refinamento de tipos**: Especificação como tipo → programa por construção
- **Ferramentas**: Leon (Scala), Synquid, F* (Dafny-style)

---

## Referências de Acompanhamento

| Área | Venues / Fontes |
|------|----------------|
| Verificação/ITP | ITP, CPP, FLOC, Lean/Coq/Agda Zulip |
| HoTT/Univalent | HoTT/UF workshop, nLab, Cubical Agda repo |
| Effect Systems | ICFP, PLDI, Koka/Eff/OCaml multicore |
| Linear Types | POPL, PLDI, Rust/Linear Haskell |
| Quantum | QIP, TQC, Quantum Journal |
| Synthesis | CAV, PLDI, SyGuS-Comp, ARC leaderboard |

---

*Próximo: [Exercícios Práticos](exercises.md) | [Paradigmas](../paradigms/concept.md)*