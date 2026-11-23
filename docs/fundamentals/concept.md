# Fundamentos Matemáticos e Computacionais

## Visão Geral

Esta fase cobre as bases teóricas que sustentam toda a computação: lógica, teoria de conjuntos, teoria de categorias, teoria de domínios, lambda calculus, máquinas de Turing, álgebras de processos e teoria de complexidade.

---

## Lógica Matemática

### Lógica Proposicional e de Predicados
- **Conectivos**: ∧ (e), ∨ (ou), ¬ (não), → (implica), ↔ (equivalente)
- **Tabelas-verdade**, equivalências (De Morgan, distributividade, etc.)
- **Quantificadores**: ∀ (para todo), ∃ (existe)
- **Cálculo de Sequentes** (Gentzen): regras de introdução/eliminação, cut-elimination
- **Dedução Natural**: provas diretas, por contraposição, por contradição

### Teoria de Conjuntos (ZFC)
- **Axiomas**: Extensionalidade, Par, União, Potência, Infinito, Substituição, Fundação, Escolha
- **Ordinais**: números ordinais, aritmética ordinal, indução transfinita
- **Cardinais**: cardinalidade, hipótese do continuum, álgebra cardinal
- **Axioma da Escolha**: equivalentes (Lema de Zorn, Bem-ordenação, Tychonoff)

### Teoria de Categorias
- **Objetos e Morfismos**: composição associativa, identidades
- **Funtores**: covariantes, contravariantes, preservam estrutura
- **Transformações Naturais**: morfismos entre funtores
- **Adjunctions**: adjunção livre/esquecimento, currying como adjunção
- **Mônadas**: mônada de estado, Maybe, List, IO; leis de mônada
- **Limites e Colimites**: produtos, coprodutos, pullbacks, pushouts

### Teoria de Domínios
- **CPOs** (Complete Partial Orders): elementos compactos, base, continuidade
- **Funções Contínuas**: preservam suprema de cadeias direcionadas
- **Pontos Fixos**: teorema de Kleene, menor ponto fixo, recursão
- **Topologia de Scott**: conjuntos abertos de Scott, continuidade topológica

### Lambda Calculus
- **Não Tipado**: β-redução, η-conversão, formas normais, teorema de Church-Rosser
- **Simplesmente Tipado (STLC)**: sistema de tipos, normalização forte, correspondência Curry-Howard
- **System F** (Polimorfismo de Segunda Ordem): tipos universais, quantificação, erasure
- **System F-omega**: operadores de tipo, kinds
- **Calculus of Constructions**: tipos dependentes, Π-types, Σ-types, tipos indutivos

### Modelos de Computação
- **Máquinas de Turing**: determinísticas, não-determinísticas, multi-fitas, oracle
- **Máquinas de Registradores**: Minsky, RAM, contador
- **Funções Recursivas**: recursão primitiva, μ-recursão, teorema de Kleene
- **Π-Calculus / CCS / CSP**: álgebras de processos, bisimulação, equivalência

### Teoria de Complexidade
- **Hierarquias**: Time/Space Hierarchy Theorems, P, NP, PH, PSPACE, EXP
- **P vs NP**: completude NP, reduções polinomiais, NP-intermediário (Ladner)
- **Complexidade Parametrizada**: FPT, W-hierarchy, kernelization
- **Análise de Caso Médio**: distribuições, smoothed analysis (Spielman-Teng)
- **Complexidade Quântica**: BQP, QMA, complexidade de consulta quântica

---

## Aplicações Práticas

| Conceito | Aplicação em Engenharia |
|----------|------------------------|
| Lógica/Sequentes | Verificação formal, SMT solvers, provadores de teoremas |
| Teoria de Categorias | Design de APIs, arquitetura funcional, mônadas em Haskell/Scala |
| Teoria de Domínios | Semântica de linguagens, recursão, ponto fixo em compiladores |
| Lambda Calculus | Compiladores, inferência de tipos, linguagens funcionais |
| Complexidade | Análise de algoritmos, otimização, criptografia |

---

## Referências Essenciais

- **Pierce, B.** *Types and Programming Languages* (MIT Press)
- **Abramsky & Jung** *Domain Theory* (Handbook of Logic in CS)
- **Mac Lane** *Categories for the Working Mathematician* (Springer)
- **Barendregt** *The Lambda Calculus* (North-Holland)
- **Arora & Barak** *Computational Complexity* (Cambridge)
- **Nielson & Nielson** *Semantics with Applications* (Wiley)

---

*Próximo: [Implementações de Referência](implementation.md) → [Trade-offs](tradeoffs.md) → [Fronteiras](frontiers.md)*