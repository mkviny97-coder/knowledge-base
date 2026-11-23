# Workflow de Skills para Agentes IA

## Visão Geral

O projeto utiliza o framework **ECC (Everything Claude Code)** com skills organizadas em 5 fases sequenciais. Cada fase possui skills específicas que os agentes devem invocar via slash commands.

---

## 1. Fase de Planejamento (O Arquiteto)

**NUNCA deixe a IA começar a escrever código sem antes passar por aqui.**

| Comando | Descrição |
|---------|-----------|
| `/ecc:plan` | Plano de implementação simples e direto |
| `/ecc:blueprint` | Projetos complexos: mapa técnico detalhado, arquitetura, dependências |
| `/ecc:architecture-decision-records` | Registrar decisões técnicas (essencial para projetos que crescem) |

---

## 2. Fase de Implementação (O Desenvolvedor)

**Onde o código nasce. Use estas skills para garantir código profissional.**

| Comando | Descrição |
|---------|-----------|
| `/ecc:prp-implement` | **Skill "Ouro"**. Implementação profissional com rigor técnico |
| `/ecc:feature-dev` | Adicionar funcionalidade nova em projeto existente |
| `/ecc:tdd-workflow` | Test-Driven Development: testes ANTES do código |

---

## 3. Fase de Revisão e Qualidade (O QA/Reviewer)

**Essencial para evitar bugs em produção. Chame APÓS o código ser escrito.**

| Comando | Descrição |
|---------|-----------|
| `/ecc:code-review` | Revisão padrão: bugs, performance, padronização |
| `/ecc:orch-review` | Revisão "adversária" profunda: múltiplos especialistas |
| `/ecc:verification-loop` | **Check final**: build, lint, testes, segurança → PASS/FAIL |

---

## 4. Fase de Manutenção e Correção (O Debugger)

**Para quando algo quebra ou o código ficou "sujo".**

| Comando | Descrição |
|---------|-----------|
| `/ecc:build-fix` | Erro de compilação/TypeScript/Dependências: fix mínimo |
| `/ecc:refactor-clean` | Remove código morto, simplifica estrutura sem mudar comportamento |

---

## 5. Fase de Infraestrutura e Entrega (O DevOps)

**Para tirar o código da máquina e colocar no ar.**

| Comando | Descrição |
|---------|-----------|
| `/ecc:deployment-patterns` | CI/CD, Docker, estratégias de deploy |
| `/ecc:terraform-patterns` | Infrastructure as Code (AWS, Azure, GCP) |

---

## Combo Perfeito — Sequência Exata para Qualquer Tarefa

Para resultado máximo, chame os agentes nesta sequência:

```bash
1. PLANEJAR: /ecc:blueprint          → (Aprove o plano gerado)
2. CODAR:    /ecc:prp-implement      → (Gere o código)
3. REVISAR:  /ecc:code-review        → (Corrija os pontos apontados)
4. VALIDAR:  /ecc:verification-loop  → (Confirme que tudo está verde)
```

---

## Dica Extra: Skills Específicas por Linguagem

**Sempre chame a skill da linguagem JUNTO com a de implementação** para que a IA use os padrões mais modernos daquela tecnologia:

| Stack | Comando Combinado |
|-------|-------------------|
| React/Next.js | `/ecc:react-patterns` + `/ecc:prp-implement` |
| Python | `/ecc:python-patterns` + `/ecc:prp-implement` |
| Kotlin/KMP | `/ecc:kotlin-patterns` + `/ecc:prp-implement` |
| Rust | `/ecc:rust-patterns` + `/ecc:prp-implement` |
| Go | `/ecc:go-patterns` + `/ecc:prp-implement` |
| TypeScript | `/ecc:typescript-patterns` + `/ecc:prp-implement` |
| Java/Spring/Quarkus | `/ecc:java-patterns` + `/ecc:prp-implement` |
| C++ | `/ecc:cpp-patterns` + `/ecc:prp-implement` |
| Swift/SwiftUI | `/ecc:swift-patterns` + `/ecc:prp-implement` |
| Dart/Flutter | `/ecc:dart-flutter-patterns` + `/ecc:prp-implement` |

**Outras skills de linguagem disponíveis:**
- `/ecc:django-patterns`, `/ecc:laravel-patterns`, `/ecc:rails-patterns`
- `/ecc:nuxt4-patterns`, `/ecc:vue-patterns`, `/ecc:angular-developer`
- `/ecc:zig-patterns`, `/ecc:carbon-patterns`, `/ecc:mojo-patterns`

---

## Como os Agentes Devem Usar Estas Skills na Prática

### Exemplo 1 — Nova funcionalidade em projeto React existente
```bash
1. Arquiteto: /ecc:feature-dev (entende o codebase) → /ecc:plan (plano)
2. Dev:       /ecc:react-patterns + /ecc:prp-implement (implementa)
3. QA:        /ecc:code-review → /ecc:verification-loop
4. Se falhar build: Debugger: /ecc:build-fix
```

### Exemplo 2 — Novo microserviço Go do zero
```bash
1. Arquiteto: /ecc:blueprint (arquitetura completa) → ADR via /ecc:architecture-decision-records
2. Dev:       /ecc:go-patterns + /ecc:prp-implement (código + testes via /ecc:tdd-workflow)
3. QA:        /ecc:orch-review (revisão profunda) → /ecc:verification-loop
4. DevOps:    /ecc:deployment-patterns (Docker, CI/CD) → /ecc:terraform-patterns (infra)
```

### Exemplo 3 — Refatoração de legacy Python
```bash
1. Arquiteto: /ecc:plan (escopo da refatoração)
2. Dev:       /ecc:python-patterns + /ecc:prp-implement (código novo)
3. Debugger:  /ecc:refactor-clean (remove dead code)
4. QA:        /ecc:code-review → /ecc:verification-loop
```

### Exemplo 4 — Bug crítico em produção
```bash
1. Debugger:  /ecc:build-fix (se erro de build) ou análise manual
2. Dev:       /ecc:prp-implement (fix com teste via /ecc:tdd-workflow)
3. QA:        /ecc:verification-loop (valida fix)
4. DevOps:    /ecc:deployment-patterns (hotfix deploy)
```

---

## Regras de Ouro para os Agentes

1. **NUNCA** pule a fase de planejamento. Sem plano aprovado, não há código.
2. **SEMPRE** use `/ecc:prp-implement` para código de produção (não `/ecc:plan` sozinho).
3. **SEMPRE** rode `/ecc:verification-loop` antes de considerar tarefa completa.
4. **SEMPRE** invoque skill de linguagem específica junto com implementação.
5. Para revisão crítica: use `/ecc:orch-review` (adversarial) em vez de `/ecc:code-review`.
6. Registre decisões arquiteturais com `/ecc:architecture-decision-records`.
7. Mantenha ADRs atualizados — são memória do projeto.
8. Se código não compila: `/ecc:build-fix` primeiro, só depois revisão.
9. Periodicamente: `/ecc:refactor-clean` para evitar debt técnico.
10. Documente o "porquê" nas ADRs, não só o "o quê".

---

*Próximo: [Referência de Arquivos](reference.md) → [Trilhas de Aprendizado](learning_paths.md)*