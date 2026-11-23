# Exercícios Práticos — Fundamentos

## Lógica

### Exercício 1: Tautologias
Prove que as seguintes são tautologias usando dedução natural:
1. `p → (q → p)`
2. `(p → (q → r)) → ((p → q) → (p → r))`
3. `((p → q) → p) → p` (Lei de Peirce)

**Solução esboço (1)**:
```
1. p          [suposição]
2.   q        [suposição]
3.   p        [reiteração 1]
4.   q → p    [→I 2-3]
5. p → (q → p) [→I 1-4]
```

### Exercício 2: Normalização
Converta para CNF: `¬(p ∨ q) → (r ∧ ¬s)`

**Resposta**: `(p ∨ r) ∧ (p ∨ ¬s) ∧ (q ∨ r) ∧ (q ∨ ¬s)`

---

## Teoria de Categorias

### Exercício 3: Leis de Mônada
Verifique as três leis para `Maybe`:
1. **Left identity**: `return a >>= f ≡ f a`
2. **Right identity**: `m >>= return ≡ m`
3. **Associativity**: `(m >>= f) >>= g ≡ m >>= (λx → f x >>= g)`

### Exercício 4: Adjunção
Prove que `List` é livre sobre `Set`: `Hom_Mon(List A, M) ≅ Hom_Set(A, U M)`

---

## Lambda Calculus

### Exercício 5: β-redução
Reduza a forma normal:
```
(λx. λy. x) (λz. z z) (λw. w)
```

**Passos**:
1. `(λy. (λz. z z)) (λw. w)`  [β na aplicação externa]
2. `λz. z z`                   [β na aplicação interna]

### Exercício 6: Tipagem STLC
Encontre o tipo principal de: `λf. λx. f (f x)`

**Resposta**: `(α → α) → α → α` (tipo Church numeral)

---

## Complexidade

### Exercício 7: Redução 3-SAT
Converta a cláusula `(x₁ ∨ x₂ ∨ x₃ ∨ x₄)` para 3-SAT introduzindo variáveis auxiliares.

**Resposta**: `(x₁ ∨ x₂ ∨ y₁) ∧ (¬y₁ ∨ x₃ ∨ x₄)`

### Exercício 8: Hierarquia de Tempo
Use o teorema da hierarquia de tempo para mostrar que existe linguagem em `DTIME(n²)` mas não em `DTIME(n)`.

**Ideia**: Diagonalização sobre máquinas que param em tempo `n`.

---

## Projetos de Implementação

### Projeto 1: Mini Prover (Python)
Implemente um provador de lógica proposicional usando:
- Cálculo de sequentes (G3cp)
- Busca em profundidade com backtracking
- Heurística: escolher fórmula mais complexa

### Projeto 2: STLC Type Checker (TypeScript)
Implemente inferência bidirecional (check/synth) para STLC com:
- Variáveis de tipo metavariáveis
- Unificação com ocorre-check
- Mensagens de erro com contexto

### Projeto 3: Category Theory Library (Rust)
Implemente:
- `Functor`, `Applicative`, `Monad` traits
- `List`, `Option`, `Result` instances
- Leis como testes (quickcheck)

---

## Recursos para Prática

| Plataforma | Foco |
|------------|------|
| **Lean 4** | Teoria de tipos dependentes, mathlib |
| **Coq** | Provas certificadas, extração de código |
| **Agda** | Programação dependente, cubical |
| **Haskell** | Categorias aplicadas, type families |
| **Rust** | Linear types, ownership, traits |
| **Koka** | Algebraic effects, handlers |

---

*Próximo: [Paradigmas de Programação](../paradigms/concept.md)*