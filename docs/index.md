# Knowledge Base de Programação

**Base de conhecimento completa para desenvolvimento de software** — cobrindo fundamentos matemáticos, paradigmas de programação, algoritmos, internals de linguagem, concorrência e sistemas distribuídos.

---

## 📚 Estrutura do Repositório

```
knowledge-base/
├── fundamentals/           # Fase 1: Fundamentos Matemáticos e Computacionais
├── paradigms/              # Fase 2: Paradigmas de Programação (Taxonomia Completa)
├── algorithms/             # Fase 3: Estruturas de Dados e Algoritmos (Core + Avançado)
├── language-internals/     # Fase 4: Internals de Linguagem (Compiladores, Runtime, GC, Type Systems)
└── concurrency/            # Fase 5: Concorrência, Paralelismo e Sistemas Distribuídos
```

---

## 🎯 Objetivo

Esta knowledge base é projetada para ser **A FUNDAÇÃO PARA QUALQUER TAREFA DE PROGRAMAÇÃO**. Seja construindo um compilador, banco de dados, sistema distribuído, game engine, plataforma ML, ou aprendendo um novo paradigma — as fundamentações teóricas e implementações de referência aqui fornecem o entendimento profundo necessário para:

1. **Tomar decisões arquiteturais corretas**
2. **Implementar soluções eficientes**
3. **Raciocinar sobre correção**
4. **Ensinar qualquer aspecto de programação a outros modelos/agentes**

---

## 🚀 Início Rápido

### Navegação por Fase

| Fase | Tópico | Descrição |
|------|--------|-----------|
| **1** | [Fundamentos](fundamentals/concept.md) | Lógica, conjuntos, categorias, teoria de tipos, lambda calculus |
| **2** | [Paradigmas](paradigms/concept.md) | Imperativo, OO, Funcional, Lógico, Concorrente, Metaprogramação |
| **3** | [Algoritmos](algorithms/concept.md) | 25+ tópicos: sorting, grafos, DP, paralelos, quânticos, streaming |
| **4** | [Internals](language-internals/concept.md) | Compiladores, type systems, IR, GC (9 algoritmos), VM/JIT, semântica formal |
| **5** | [Concorrência](concurrency/concept.md) | Thread models, sync, memory models, lock-free, consensus (Paxos/Raft), actors |

---

## 🛠 Workflow de Skills para Agentes IA

O projeto utiliza o framework **ECC (Everything Claude Code)** com skills organizadas em 5 fases sequenciais:

### Combo Perfeito — Sequência Exata
```bash
1. PLANEJAR: /ecc:blueprint     → (Aprove o plano)
2. CODAR:    /ecc:prp-implement → (Gere o código)
3. REVISAR:  /ecc:code-review   → (Corrija pontos)
4. VALIDAR:  /ecc:verification-loop → (Confirme PASS)
```

Ver [guia completo de workflow](skills/workflow.md).

---

## 📖 Como Usar Esta Documentação

- **Busca**: Use a busca no topo (suporta operadores `+`, `-`, `"`)
- **Navegação**: Abas no topo organizam por fase; sidebar expande seções
- **Código**: Todos os blocos têm botão de copiar; abas para múltiplas linguagens
- **Tema**: Toggle claro/escuro no canto superior direito
- **Versões**: Seletor de versão no rodapé (quando configurado)

---

## 📊 Cobertura Atual

| Categoria | Arquivos | Linhas (aprox) | Status |
|-----------|----------|----------------|--------|
| Fundamentos | 6 | ~5.000 | ✅ Completo |
| Paradigmas | 6 | ~8.000 | ✅ Completo |
| Algoritmos | 28 | ~15.000 | ✅ Completo |
| Internals | 7 | ~12.000 | ✅ Completo |
| Concorrência | 13 | ~10.000 | ✅ Completo (Fases 6-9 planejadas) |

**Total**: ~50.000 linhas de conteúdo técnico estruturado

---

## 🔗 Links Úteis

- [Guia de Referência Rápida](skills/reference.md) — Qual arquivo ler para cada necessidade
- [Trilhas de Aprendizado](skills/learning_paths.md) — Iniciante → Expert
- [Princípios de Desenvolvimento](about/principles.md) — Qualidade, arquitetura, performance
- [Fases Futuras](about/future_phases.md) — Roadmap Fases 6-9

---

## 📝 Licença e Contribuição

Este projeto é mantido como base de conhecimento para desenvolvimento de software. Consulte o repositório original para detalhes de licença e contribuição.

---

*Gerado em: 2026-11-22 | Última atualização: {{ git_revision_date_localized }}*