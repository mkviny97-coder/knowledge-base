# Notas de Manutenção

## Versão Atual
**Estado em**: 2026-11-22  
**Versão**: 1.0.0 (Fases 1-5 completas)

---

## Atualizações Futuras

Novas fases serão adicionadas ao diretório `knowledge-base/` conforme planejado:

```
knowledge-base/
├── fundamentals/           # Fase 1 ✓
├── paradigms/              # Fase 2 ✓
├── algorithms/             # Fase 3 ✓
├── language-internals/     # Fase 4 ✓
├── concurrency/            # Fase 5 ✓
├── architecture/           # Fase 6 (planejada)
├── specialized-domains/    # Fase 7 (planejada)
├── frontier/               # Fase 8 (planejada)
└── ai-training/            # Fase 9 (planejada)
```

---

## Cross-References

Arquivos referenciam uns aos outros via **caminhos relativos**:

- `../fundamentals/concept.md`
- `../../algorithms/graph_algos.md`
- `./tradeoffs.md`

**Regra**: Sempre use caminhos relativos a partir do arquivo atual. Não use caminhos absolutos.

---

## Testes

Quando test suite for adicionado:

```bash
# Executar todos os testes
python -m pytest knowledge-base/

# Ou por fase
python -m pytest knowledge-base/fundamentals/
python -m pytest knowledge-base/algorithms/
```

### Estrutura de Testes Esperada
```
knowledge-base/
├── fundamentals/
│   ├── test_concept.py
│   └── test_implementation.py
├── algorithms/
│   ├── test_sorting.py
│   ├── test_graph_algos.py
│   └── ...
└── conftest.py              # Fixtures compartilhadas
```

---

## Documentação

Cada fase segue estrutura padronizada:

| Arquivo | Propósito |
|---------|-----------|
| `concept.md` | Teoria, definições, visão geral |
| `implementation.md` | Padrões de implementação, código de referência |
| `tradeoffs.md` | Critérios de decisão, quando usar cada abordagem |
| `frontiers.md` | Pesquisa atual, tópicos abertos, venuse |
| `exercises.md` | Problemas práticos, projetos capstone |
| `references.bib` | Bibliografia em formato BibTeX |

---

## Convenções de Escrita

### Código
- **Python**: type hints completos, docstrings Google/NumPy style
- **Rust**: `///` docs, `#[doc = "..."]` para módulos
- **TypeScript**: JSDoc + types, strict mode
- **Complexidade**: sempre anotada em docstring

### Matemática
- **LaTeX math**: `$O(n \log n)$`, `$\Theta(n^2)$`
- **Unicode**: `→`, `∀`, `∃`, `∧`, `∨`, `¬`, `≠`, `≤`, `≥`
- **Notação**: consistente com literatura padrão (CLRS, TAPL, DDIA)

### Diagramas
- **Mermaid** para diagramas renderizáveis no MkDocs
- **ASCII** para tabelas e estruturas simples
- **GraphViz/D2** para diagramas complexos (exportar SVG)

---

## Processo de Contribuição

### Adicionando Novo Conteúdo
1. Identifique a fase e tópico corretos
2. Crie arquivo seguindo template da fase
3. Adicione entrada no `mkdocs.yml` → `nav`
4. Atualize `skills/reference.md` se novo arquivo principal
5. Rode `mkdocs build` para verificar links

### Atualizando Conteúdo Existente
1. Edite arquivo alvo
2. Verifique cross-references não quebrados
3. Atualize `frontiers.md` da fase se novo research
4. Considere ADR se mudança arquitetural

### Versionamento
- **SemVer**: MAJOR.MINOR.PATCH
- **CHANGELOG.md**: maintain a changelog
- **Git tags**: `v1.0.0`, `v1.1.0`, etc.

---

## Métricas de Qualidade

| Métrica | Target |
|---------|--------|
| Cobertura de tópicos (Fases 1-5) | 100% |
| Arquivos com `implementation.md` | 100% |
| Exemplos de código compiláveis | 100% |
| Links internos válidos | 100% |
| Build MkDocs sem warnings | ✅ |

---

## Deploy da Documentação

### Local
```bash
pip install mkdocs-material mkdocs-git-revision-date-localized-plugin mkdocs-minify-plugin mkdocs-macros-plugin pymdown-extensions
mkdocs serve
# Abre em http://localhost:8000
```

### Produção (GitHub Pages)
```bash
mkdocs gh-deploy --force
```

### CI/CD (GitHub Actions)
Ver `.github/workflows/docs.yml` (criar conforme deployment-patterns skill)

---

## Checklist de Release

- [ ] `mkdocs build` passa sem erros
- [ ] Todos os links internos funcionam
- [ ] Navegação lateral completa
- [ ] Busca indexa todo conteúdo
- [ ] Tema claro/escuro OK
- [ ] Mobile responsivo
- [ ] PDF export (opcional): `mkdocs build --strict && mkdocs pdf` (se plugin)

---

*Próximo: [Workflow de Skills](../skills/workflow.md) | [Referência Rápida](../skills/reference.md)*