# Paradigmas de Programação — Taxonomia Completa

## Visão Geral

Esta fase cataloga e compara os principais paradigmas de programação, fornecendo critérios para escolha baseada no problema, equipe e restrições.

---

## 1. Paradigma Imperativo

### Características
- **Estado mutável** como mecanismo principal
- **Controle de fluxo**: sequenciamento, condicionais, loops, goto
- **Procedimentos/Subrotinas**: abstração de controle
- **Módulos**: encapsulamento de estado e operações

### Linguagens Representativas
C, Pascal, Ada, Go, Rust (parcial), Python (parcial)

### Padrões Clássicos (GoF)
- **Criacionais**: Factory, Builder, Singleton, Prototype
- **Estruturais**: Adapter, Decorator, Facade, Composite, Proxy
- **Comportamentais**: Strategy, Observer, Command, State, Template Method

### Princípios SOLID
- **S**ingle Responsibility
- **O**pen/Closed
- **L**iskov Substitution
- **I**nterface Segregation
- **D**ependency Inversion

### GRASP
Information Expert, Creator, Controller, Low Coupling, High Cohesion, Polymorphism, Pure Fabrication, Indirection, Protected Variations

---

## 2. Paradigma Orientado a Objetos

### Pilares
- **Encapsulamento**: dados + comportamento juntos, visibilidade controlada
- **Herança**: reutilização + polimorfismo (single/multiple, interface vs implementação)
- **Polimorfismo**: dispatch dinâmico, substituição (LSP)
- **Abstração**: interfaces, classes abstratas

### Modelos de Objeto
- **Baseado em Classes** (Simula, C++, Java, C#): classes como factories
- **Baseado em Protótipos** (Self, JavaScript, Lua): objetos clonam objetos
- **Traits/Composição** (Scala, Rust, Go): composição sobre herança

### Dispatch
- **Single dispatch**: `obj.method(args)` — receptor determina método
- **Multiple dispatch** (Julia, CLOS): todos os args determinam método
- **Predicate dispatch**: dispatch em condições arbitrárias

---

## 3. Paradigma Funcional

### Princípios Fundamentais
- **Funções puras**: mesmo input → mesmo output, sem efeitos colaterais
- **Imutabilidade**: estruturas de dados persistentes
- **Higher-order functions**: funções como valores de primeira classe
- **Recursão** no lugar de loops
- **Expressões** em vez de statements

### Abstrações Algébricas
| Abstração | Lei Principal | Exemplo |
|-----------|---------------|---------|
| **Functor** | `map (f ∘ g) = map f ∘ map g` | `List`, `Option`, `Future` |
| **Applicative** | `pure f <*> pure x = pure (f x)` | Paralelismo, validação |
| **Monad** | `return a >>= f = f a` | `IO`, `State`, `Either` |
| **Traversable** | `traverse f = sequence ∘ map f` | Efeitos em estruturas |

### Sistemas de Efeitos
- **Monad Transformers**: `StateT s (ExceptT e IO) a`
- **Algebraic Effects** (Koka, Eff, OCaml 5): handlers composíveis
- **Effect Rows** (Row polymorphism): extensibilidade

### Tipos Lineares/Afinés
- **Linear** (usado exatamente 1x): Rust ownership, Clean
- **Afiné** (usado ≤ 1x): Rust `Drop`, recursos
- **Relevante** (usado ≥ 1x): contração controlada

---

## 4. Paradigma Lógico/Relacional

### Prolog / Datalog
- **Cláusulas de Horn**: `Head :- Body₁, Body₂, ...`
- **Unificação**: algoritmo de Robinson
- **Backtracking**: busca em profundidade com choice points
- **Cut (!)**: controle de backtracking

### Constraint Logic Programming (CLP)
- **Domínios**: FD (finito), R (reais), Bool (SAT)
- **Propagação de restrições**: arc consistency (AC-3)
- **Labeling**: busca de soluções

### Answer Set Programming (ASP)
- **Semântica de modelos estáveis** (Gelfond-Lifschitz)
- **Regras com negação na cabeça**: `{a; b} :- not c.`
- **Otimização**: `#minimize`, `#maximize`

### SAT/SMT Solving
- **SAT**: Boolean satisfiability (CDCL)
- **SMT**: Satisfiability Modulo Theories (Nelson-Oppen)
- **Teorias**: LIA (linear arithmetic), BV (bitvectors), Arrays, UF

---

## 5. Paradigma Concorrente

### Modelo de Atores (Hewitt/Agha/Erlang)
- **Atores**: estado privado + mailbox + comportamento
- **Mensagens assíncronas**: `send`, `receive`
- **Supervisão**: árvores de falha (OTP)
- **Location transparency**: mesmo código local/remoto

### CSP (Hoare) / π-Calculus
- **Processos**: `P ::= 0 | a.P | P+Q | P|Q | (νa)P | !P`
- **Canais**: síncronos (rendezvous) ou assíncronos
- **Bisimulação**: equivalência comportamental
- **Session Types**: protocolos tipados em canais

### Join Calculus
- **Definições de join**: `join { p(x) & q(y) → r(x,y) }`
- **Implementação eficiente**: compilação para máquinas de estado

---

## 6. Paradigma Metaprogramação

### Macros
- **Lisp-style** (homoicônico): código = dados (AST), `quote`, `quasiquote`, `unquote`
- **Rust proc-macros**: funções `TokenStream → TokenStream`
- **Julia @generated**: especialização em tempo de compilação
- **Template Haskell**: splicing, quotes

### Reflection
- **Introspecção**: `typeof`, `getFields`, `invoke`
- **Intercessão**: modificar estrutura em runtime
- **Mirrors** (Newspeak): separação reflexão/objeto

### Staging / Multi-stage Programming
- **Níveis**: `□` (code), `◊` (run)
- **Exemplos**: MetaOCaml, Terra, Squid (Scala)

### Compile-time Computation
- **Constexpr** (C++), **comptime** (Zig), **const eval** (Rust)
- **Type-level programming**: type families, GADTs, dependent types

---

## 7. Paradigma Reativo

### FRP (Functional Reactive Programming)
- **Signals/Behaviors**: `Time → Value` (contínuo)
- **Events**: `Time → Maybe Value` (discreto)
- **Switching**: `switch : Event (Signal a) → Signal a`

### Streams / Observables (Rx)
- **Push-based**: `Observable<T>` + operators (map, filter, flatMap)
- **Backpressure**: `Flowable`, `AsyncIterator`, Reactive Streams spec
- **Hot vs Cold**: compartilhamento vs re-execução

### Synchronous Dataflow (Lustre, Esterel)
- **Relógio lógico**: ticks discretos
- **Causalidade**: saída no mesmo tick que entrada
- **Compilação para autômatos**: código C determinístico

---

## 8. Paradigma Probabilístico

### Probabilistic Programming
- **Modelo**: `model { x ~ Normal(0,1); observe(y | x) }`
- **Inferência**: MCMC (NUTS, HMC), Variational (SVI), SMC
- **Linguagens**: Stan, Pyro, NumPyro, Gen, Turing.jl, Anglican

### Bayesian Inference
- **Prior → Likelihood → Posterior**
- **Conjugacy**: analítico (Beta-Binomial, Normal-Normal)
- **Aproximação**: Laplace, EP, VI

---

## Matriz de Decisão: Escolhendo o Paradigma

| Problema | Paradigma Recomendado | Rationale |
|----------|----------------------|-----------|
| Sistema de tempo real, embedded | Imperativo + Rust/C | Controle de memória, latência |
| Regras de negócio complexas | Funcional + DDD | Pureza, testabilidade, composição |
| UI/Event-driven | Reativo (Rx, Signals) | Propagação de mudanças, async |
| Concorrência massiva | Atores (Erlang/Akka) / CSP (Go) | Isolamento, supervisão |
| Prova de correção | Funcional + Tipos Dependentes | Curry-Howard, extração |
| Busca/otimização | Lógico (ASP, CP-SAT) | Declarativo, solvers poderosos |
| Metaprogramação pesada | Lisp / Rust macros / Zig comptime | Homoicidade / tempo de compilação |
| ML/Inferência Bayesiana | Probabilístico (Pyro, Stan) | Inferência automática |

---

## Híbridos Modernos

- **Rust**: Imperativo + Funcional (iterators, closures) + Linear Types + Macros
- **Scala**: OO + Funcional + Macros + Type Classes
- **Kotlin**: OO + Funcional + Coroutines + DSLs
- **Swift**: OO + Funcional (protocol-oriented) + Actors + Macros
- **F#**: Funcional-first + OO + Type Providers + Computation Expressions
- **OCaml 5**: Funcional + Algebraic Effects + Multicore

---

*Próximo: [Fundamentos](../fundamentals/concept.md) | [Algoritmos](../algorithms/concept.md) | [Internals de Linguagem](../language-internals/concept.md) | [Concorrência](../concurrency/concept.md)*