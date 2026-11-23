# Trade-offs de Design — Fundamentos

## Lógica: Sequentes vs Dedução Natural

| Critério | Cálculo de Sequentes | Dedução Natural |
|----------|---------------------|-----------------|
| **Provas** | Estruturadas, simétricas | Intuitivas, próximas do raciocínio humano |
| **Automação** | Melhor para provadores (cut-elimination) | Requer heurísticas para busca |
| **Meta-teoria** | Subfórmula property, consistência direta | Normalização mais complexa |
| **Uso prático** | Coq (kernel), Lean, provadores SMT | Provas humanas, ensino |

**Recomendação**: Use **Sequentes** para kernels de provadores; **Dedução Natural** para interface com humanos.

---

## Teoria de Conjuntos vs Teoria de Tipos

| Aspecto | ZFC (Conjuntos) | Teoria de Tipos (MLTT, CoC) |
|---------|----------------|----------------------------|
| **Fundação** | Única, tudo é conjunto | Estruturada, tipos como cidadãos de primeira classe |
| **Computação** | Não construtiva por default | Construtiva (Curry-Howard) |
| **Extração de código** | Difícil | Direta (programas = provas) |
| **Universos** | Classes próprias | Hierarquia de universos (Type₀ : Type₁ : ...) |
| **Ferramentas** | Mizar, Isabelle/ZF | Coq, Agda, Lean, Idris |

**Trade-off**: ZFC para matemática clássica; Teoria de Tipos para **programas verificados** e extração de código executável.

---

## Categorias vs Teoria de Conjuntos como Fundação

- **Categorias (ETCS/Univalent Foundations)**: Estrutura-preservação nativa, isomorfismo = igualdade (univalência)
- **Conjuntos (ZFC)**: Membro ∈ como primitiva, extensionalidade
- **Prática**: Linguagens funcionais modernas (Haskell, Scala) usam padrões categóricos (funtores, mônadas) sem fundação categórica formal

---

## Lambda Calculus: Tipado vs Não Tipado

| Propriedade | Não Tipado | STLC | System F | Dependent Types |
|-------------|------------|------|----------|-----------------|
| **Expressividade** | Turing-completo | Não (sem recursão geral) | Polimorfismo paramétrico | Tipos dependem de valores |
| **Normalização** | Não (loop infinito) | Forte | Forte | Forte (com restrições) |
| **Decidibilidade** | Indecidível | Decidível | Decidível (inferência undecidível) | Semi-decidível |
| **Uso** | Teoria, Lisp/Scheme | ML, Haskell (base) | Haskell (RankNTypes), Rust (generics) | Idris, Agda, Lean, Coq |

**Regra prática**: Quanto mais expressivo o sistema de tipos, mais difícil a inferência e mais anotações necessárias.

---

## Modelos de Computação

| Modelo | Melhor Para | Limitações |
|--------|-------------|------------|
| **Turing Machine** | Teoria de complexidade, decidibilidade | Baixo nível, tedioso para programar |
| **Lambda Calculus** | Semântica de linguagens, compiladores | Abstrato, não modela memória/estado |
| **Registradores/RAM** | Análise de algoritmos realista | Dependente de arquitetura |
| **π-Calculus** | Concorrência, protocolos distribuídos | Complexo, ferramentas limitadas |

---

## Complexidade: P vs NP na Prática

| Abordagem | Quando Usar |
|-----------|-------------|
| **Algoritmo exato (exp)** | Instâncias pequenas (n ≤ 20-30), n pequeno |
| **Aproximação (PTAS/FPTAS)** | NP-hard, precisa garantia de qualidade |
| **FPT (parâmetro k)** | Problema FPT, k pequeno na prática |
| **Heurísticas/SAT solvers** | Instâncias industriais, sem garantia |
| **Quântico (Grover/QAOA)** | Futuro: busca não-estruturada, otimização |

---

## Resumo: Escolhendo a Fundação Certa

```
Precisa extrair código executável de provas?
├── Sim → Teoria de Tipos Dependentes (Coq, Agda, Lean, Idris)
└── Não →
    ├── Matemática clássica pesada? → ZFC (Isabelle/ZF, Mizar)
    ├── Verificação de hardware/protocolos? → Lógica Temporal / Model Checking
    ├── Semântica de linguagem? → Lambda Calculus + Teoria de Domínios
    ├── Design de APIs/arquitetura funcional? → Teoria de Categorias (aplicada)
    └── Análise de complexidade? → Máquinas de Turing / RAM
```

---

*Próximo: [Fronteiras de Pesquisa](frontiers.md) → [Exercícios](exercises.md)*