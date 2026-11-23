# Implementações de Referência — Fundamentos

## Lógica e Prova

### Verificador de Tautologias (Python)
```python
from itertools import product

def eval_prop(formula: str, valuation: dict[str, bool]) -> bool:
    """Avalia fórmula proposicional sob valoração."""
    # Substitui variáveis
    for var, val in valuation.items():
        formula = formula.replace(var, str(val))
    # Operadores
    formula = formula.replace("∧", " and ").replace("∨", " or ")
    formula = formula.replace("¬", " not ").replace("→", " <= ")
    formula = formula.replace("↔", " == ")
    return eval(formula)

def is_tautology(formula: str, vars: list[str]) -> bool:
    return all(eval_prop(formula, dict(zip(vars, vals)))
               for vals in product([False, True], repeat=len(vars)))

# Exemplo: Lei de Morgan
assert is_tautology("¬(p ∧ q) ↔ (¬p ∨ ¬q)", ["p", "q"])
```

### Normalização de Formulas (CNF/DNF)
```python
from dataclasses import dataclass
from typing import Union

@dataclass
class Var: name: str
@dataclass
class Not: expr: 'Formula'
@dataclass
class And: left: 'Formula'; right: 'Formula'
@dataclass
class Or: left: 'Formula'; right: 'Formula'
@dataclass
class Imp: left: 'Formula'; right: 'Formula'
@dataclass
class Iff: left: 'Formula'; right: 'Formula'

Formula = Union[Var, Not, And, Or, Imp, Iff]

def to_nnf(f: Formula) -> Formula:
    """Converte para Forma Normal Negativa (NNF)."""
    match f:
        case Not(Not(x)): return to_nnf(x)
        case Not(And(l, r)): return Or(to_nnf(Not(l)), to_nnf(Not(r)))
        case Not(Or(l, r)): return And(to_nnf(Not(l)), to_nnf(Not(r)))
        case Not(Imp(l, r)): return And(to_nnf(l), to_nnf(Not(r)))
        case Not(Iff(l, r)): return Or(And(to_nnf(l), to_nnf(Not(r))),
                                        And(to_nnf(Not(l)), to_nnf(r)))
        case Imp(l, r): return Or(to_nnf(Not(l)), to_nnf(r))
        case Iff(l, r): return Or(And(to_nnf(l), to_nnf(r)),
                                   And(to_nnf(Not(l)), to_nnf(Not(r))))
        case And(l, r): return And(to_nnf(l), to_nnf(r))
        case Or(l, r): return Or(to_nnf(l), to_nnf(r))
        case Not(Var(_)): return f
        case Var(_): return f

def to_cnf(f: Formula) -> Formula:
    """Converte NNF para CNF via distributividade."""
    f = to_nnf(f)
    def distribute(f: Formula) -> Formula:
        match f:
            case And(l, r): return And(distribute(l), distribute(r))
            case Or(And(l, r), x): return And(distribute(Or(l, x)), distribute(Or(r, x)))
            case Or(x, And(l, r)): return And(distribute(Or(x, l)), distribute(Or(x, r)))
            case Or(l, r): return Or(distribute(l), distribute(r))
            case _: return f
    return distribute(f)
```

---

## Teoria de Categorias em Código

### Funtores e Mônadas (TypeScript)
```typescript
// Funtor: interface genérica
interface Functor<F> {
  map<A, B>(fa: F<A>, f: (a: A) => B): F<B>;
}

// Maybe (Option) como funtor
type Maybe<A> = { kind: "some"; value: A } | { kind: "none" };

const maybeFunctor: Functor<Maybe> = {
  map: (ma, f) => ma.kind === "some" ? { kind: "some", value: f(ma.value) } : { kind: "none" }
};

// Mônada: return + bind (flatMap)
interface Monad<M> extends Functor<M> {
  of<A>(a: A): M<A>;
  chain<A, B>(ma: M<A>, f: (a: A) => M<B>): M<B>;
}

const maybeMonad: Monad<Maybe> = {
  ...maybeFunctor,
  of: (a) => ({ kind: "some", value: a }),
  chain: (ma, f) => ma.kind === "some" ? f(ma.value) : { kind: "none" }
};

// Uso: composição segura
const safeDiv = (a: number, b: number): Maybe<number> =>
  b === 0 ? { kind: "none" } : { kind: "some", value: a / b };

const result = maybeMonad.chain(
  maybeMonad.chain(maybeMonad.of(10), (x) => safeDiv(x, 2)),
  (y) => safeDiv(y, 0)
); // { kind: "none" }
```

### Adjunção Livre/Esquecimento (Rust)
```rust
// Livre: List<A> é o monóide livre sobre A
// Esquecimento: Monoid → Set esquece a estrutura

trait Monoid {
    fn empty() -> Self;
    fn combine(&self, other: &Self) -> Self;
}

impl<A> Monoid for Vec<A> {
    fn empty() -> Self { vec![] }
    fn combine(&self, other: &Self) -> Self {
        let mut v = self.clone();
        v.extend(other.clone());
        v
    }
}

// Adjunção: Free ⊣ Forget
// Hom_Monoid(Free(A), M) ≅ Hom_Set(A, Forget(M))
fn free_monoid_map<A, M: Monoid>(f: impl Fn(A) -> M) -> impl Fn(Vec<A>) -> M {
    move |list| list.into_iter().map(f).fold(M::empty(), |acc, x| acc.combine(&x))
}
```

---

## Lambda Calculus — Interpretador

### STLC com Inferência de Tipos (Python)
```python
from dataclasses import dataclass
from typing import Optional

@dataclass
class Var: name: str
@dataclass
class Lam: param: str; body: 'Term'; ty: Optional['Type'] = None
@dataclass
class App: fn: 'Term'; arg: 'Term'
Term = Var | Lam | App

@dataclass
class TVar: name: str
@dataclass
class TArr: left: 'Type'; right: 'Type'
Type = TVar | TArr

class TypeError(Exception): pass

def infer(ctx: dict[str, Type], term: Term) -> Type:
    match term:
        case Var(name):
            if name not in ctx: raise TypeError(f"Unbound: {name}")
            return ctx[name]
        case Lam(param, body, ann):
            param_ty = ann or TVar(f"${param}")
            body_ty = infer({**ctx, param: param_ty}, body)
            return TArr(param_ty, body_ty)
        case App(fn, arg):
            fn_ty = infer(ctx, fn)
            arg_ty = infer(ctx, arg)
            match fn_ty:
                case TArr(param_ty, ret_ty):
                    if not unify(param_ty, arg_ty):
                        raise TypeError("Type mismatch in application")
                    return ret_ty
                case _:
                    raise TypeError("Applying non-function")

def unify(t1: Type, t2: Type) -> bool:
    # Unificação simples (sem ocorre-check para brevidade)
    match (t1, t2):
        case (TVar(a), TVar(b)) if a == b: return True
        case (TVar(_), _) | (_, TVar(_)): return True  # Simplificado
        case (TArr(l1, r1), TArr(l2, r2)): return unify(l1, l2) and unify(r1, r2)
        case _: return False
```

---

## Teoria de Complexidade — Reduções

### SAT → 3-SAT (Redução Polinomial)
```python
def clause_to_3sat(clause: list[int]) -> list[list[int]]:
    """Converte cláusula de tamanho k em cláusulas de tamanho 3."""
    if len(clause) <= 3:
        return [clause + [0] * (3 - len(clause))]
    result = []
    # Introduz variáveis auxiliares y1, y2, ...
    for i in range(len(clause) - 2):
        if i == 0:
            result.append([clause[0], clause[1], -(i+1)])
        elif i == len(clause) - 3:
            result.append([i, clause[-2], clause[-1]])
        else:
            result.append([i, clause[i+1], -(i+2)])
    return result

# Exemplo: (x1 ∨ x2 ∨ x3 ∨ x4) → (x1 ∨ x2 ∨ ¬y1) ∧ (y1 ∨ x3 ∨ x4)
```

---

## Próximos Passos

- [Trade-offs de Design](tradeoffs.md) — Quando usar cada fundamento
- [Fronteiras de Pesquisa](frontiers.md) — Tópicos atuais
- [Exercícios Práticos](exercises.md) — Problemas resolvidos