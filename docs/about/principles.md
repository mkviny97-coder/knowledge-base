# Princípios de Desenvolvimento Incorporados em Todas as Implementações

## Qualidade de Código

### Clareza Educacional
> Prioriza **entendibilidade** sobre esperteza. Código é lido mais vezes do que escrito.

- Nomes descritivos > abreviações criptográficas
- Funções pequenas, propósito único
- Comentários explicam **POR QUÊ**, não **O QUÊ**
- Exemplos no código (tests as docs)

### Documentação Abrangente
- **Docstrings** em todas as funções/classes públicas
- **Complexidade** anotada: `O(n log n)` tempo, `O(n)` espaço
- **Invariantes** e **pré/pós-condições** explícitas
- **Exceções próprias** com mensagens acionáveis

### Testes Integrados
- Cada arquivo tem `if __name__ == "__main__":` test suite
- Property-based testing onde aplicável (Hypothesis, QuickCheck)
- Coverage ≥ 80% em código crítico
- Testes de regressão para bugs corrigidos

### Type Hints Completos
- Tipagem estática para suporte IDE e correção
- Generics, protocols, typed dicts onde apropriado
- `mypy --strict` / `pyright` / `rust-analyzer` clean

### Tratamento de Erros
- Exceções próprias hierárquicas
- Invariantes verificadas com `assert` / contratos
- Fail-fast: erro cedo, mensagem clara
- Recuperação graciosa onde faz sentido

---

## Padrões Arquiteturais

### Separação de Responsabilidades
- Módulos com **boundaries limpos** (interface/impl)
- Dependency inversion: dependa de abstrações
- Camadas: domain → application → infrastructure

### Composição sobre Herança
- **Protocols/Interfaces** > classes base
- **Strategy pattern** para comportamento variável
- **Dependency Injection** explícita (construtor/factory)

### Imutabilidade por Default
- **Functional core, imperative shell**
- Estruturas persistentes (path copying, structural sharing)
- Estado mutável isolado, explicitamente marcado

### Gerenciamento de Estado Explícito
- State machines para protocolos complexos
- Effect systems (algebraic effects) para efeitos colaterais
- Event sourcing para audit trail completo

### Observabilidade Built-in
- Métricas: latency (p50/p95/p99), throughput, error rate
- Structured logging (JSON, correlation IDs)
- Distributed tracing (W3C trace-context)
- Health checks: liveness, readiness, startup

---

## Consciência de Performance

### Anotações de Complexidade
```python
def merge_sort(arr: list[T]) -> list[T]:
    """O(n log n) tempo, O(n) espaço auxiliar.
    
    Estável. Paralelizável via merge paralelo.
    """
```

### Memory Layout Awareness
- **Cache-friendly**: arrays contíguos > linked lists
- **False sharing prevention**: padding, `#[repr(align(64))]`
- **Data-oriented design**: Structure of Arrays (SoA) > Array of Structures (AoS)

### Primitivas de Concorrência
- **Lock-free** onde apropriado (contention analysis prévio)
- **Work-stealing** para paralelismo fine-grained
- **Backpressure** em pipelines assíncronos

### Modelos de Escalabilidade
- **Amdahl's Law**: speedup limitado por parte serial
- **Gustafson's Law**: escala problema com recursos
- **Universal Scalability Law** (Gunther): contenção + coherência

---

## Aplicação Prática por Camada

| Camada | Princípios Chave |
|--------|------------------|
| **Domain** | Pure functions, value objects, invariants, no I/O |
| **Application** | Use cases, orchestration, transactions, ports |
| **Infrastructure** | Adapters, external APIs, DB, messaging, config |
| **Presentation** | Thin controllers, serialization, validation |

---

## Checklist de Code Review

- [ ] Tipos completos, sem `any`/`Any`/`interface{}`
- [ ] Testes cobrem happy path + edge cases + error paths
- [ ] Complexidade documentada
- [ ] Sem secrets hardcoded
- [ ] Logs estruturados, sem PII
- [ ] Métricas exportadas para operações críticas
- [ ] Rollback plan para mudanças de schema/migração
- [ ] Documentação atualizada (README, ADRs, docstrings)

---

*Próximo: [Fases Futuras](future_phases.md) | [Manutenção](maintenance.md)*