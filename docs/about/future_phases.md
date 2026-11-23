# Fases Futuras Planejadas (6-9)

## Fase 6: Arquitetura de Software e Engenharia Avançada

### Tópicos
- **Clean Architecture, Hexagonal, Onion Architecture**: boundaries, dependency rule, use cases
- **Domain-Driven Design (DDD)**: aggregates, entities, value objects, domain events, bounded contexts
- **Event Sourcing + CQRS**: event store, projections, snapshots, eventual consistency
- **Microservices**: service decomposition, API gateway, service mesh (Istio/Linkerd)
- **Observabilidade**: Métricas (Prometheus), Tracing (Jaeger/Zipkin), Logging (ELK/Loki), SLO/SLI
- **CI/CD, GitOps, Progressive Delivery**: ArgoCD, Flux, canary, blue-green, feature flags
- **Technical Debt Management**: arquitetura de decisão records (ADRs), refatoração contínua

### Entregáveis
```
architecture/
├── adr/                    # Architecture Decision Records
├── patterns/               # Padrões arquiteturais documentados
├── microservices/          # Templates, contracts, choreography
├── observability/          # Dashboards, alertas, runbooks
└── ci-cd/                  # Pipelines, policies, environments
```

---

## Fase 7: Domínios Especializados

### Systems Programming
- **OS Kernels**: scheduling, memory management, syscalls, interrupt handling
- **Filesystems**: VFS, journaling, copy-on-write (ZFS, Btrfs), distributed (Ceph, Gluster)
- **Networking Stack**: TCP/IP, QUIC, eBPF/XDP, DPDK, kernel bypass
- **eBPF**: verifier, maps, helpers, CO-RE, networking/observability/security

### Graphics & GPU Compute
- **Rendering Pipeline**: rasterização, ray tracing, compute shaders, mesh shaders
- **GPU Compute**: CUDA, HIP, Metal, Vulkan compute, WGPU
- **APIs Modernas**: Vulkan 1.3+, Metal 3, DirectX 12 Ultimate, WebGPU

### Cryptography
- **Primitivas**: AES-GCM, ChaCha20-Poly1305, Ed25519, BLS, hash functions (BLAKE3, SHA-3)
- **Protocolos**: TLS 1.3, Noise, Signal, WireGuard, MLS
- **Zero-Knowledge**: zk-SNARKs, zk-STARKs, PLONK, Halo2, RISC Zero
- **Post-Quantum**: ML-KEM (Kyber), ML-DSA (Dilithium), SLH-DSA (SPHINCS+)

### ML Systems
- **Training Systems**: distributed data parallel, FSDP, pipeline parallel, ZeRO
- **Inference Serving**: vLLM, TGI, TensorRT-LLM, Triton, batching, KV cache
- **Feature Stores**: Feast, Tecton, online/offline, point-in-time correctness
- **MLOps**: MLflow, Kubeflow, model registry, monitoring, drift detection

### Formal Methods
- **Theorem Provers**: Coq, Lean 4, Isabelle/HOL, Agda
- **TLA+**: especificação, model checking (TLC), refinement
- **Model Checking**: SPIN, NuSMV, IC3/PDR, CBMC
- **Verified Software**: CompCert, seL4, IronFleet, DeepSpec

---

## Fase 8: Fronteira 2024-2026+

### AI-Assisted Coding
- **Copilot/Cursor/Windsurf**: prompt engineering, context management, eval
- **Agent-based Development**: AutoGPT, Devin, SWE-agent, OpenDevin
- **Eval-driven Development**: benchmarks (SWE-bench, HumanEval), pass@k
- **Skill/Tool Learning**: continuous learning, instinct extraction

### WebAssembly
- **Components**: WASI 0.2+, component model, wit, linking
- **WASI**: preview2, sockets, http, keyvalue, blobstore, clock
- **Plugins**: extensibilidade, sandboxing, capability-based security
- **Runtimes**: wasmtime, wasmer, wasmedge, spin, fermyon

### Effect Systems
- **Koka**: effect inference, handlers, algebraic effects
- **Eff**: multilanguage, effect polymorphism
- **Algebraic Effects**: handlers, resumptions, scoped effects
- **Integration**: Rust (effectful), OCaml 5, Scala (ZIO), TypeScript (Effect)

### Quantum Programming
- **Linguagens**: Q#, Cirq, Qiskit, Silq, Quipper
- **Error Correction**: surface codes, stabilizer codes, LDPC, bosonic codes
- **NISQ Algorithms**: VQE, QAOA, quantum ML, quantum chemistry

### Novas Linguagens
| Linguagem | Foco | Status |
|-----------|------|--------|
| **Rust** | Safety, concurrency, performance | Produção |
| **Zig** | Comptime, allocators, C interop | 0.11+ |
| **Carbon** | C++ successor, migration | Experimental |
| **Vale** | Fearless concurrency, generational refs | Alpha |
| **Mojo** | Python syntax, MLIR, GPU | Early access |
| **MoonBit** | WASM-first, AI-native | Beta |

---

## Fase 9: Síntese para Treinamento de IA

### Curriculum Design
- **Spiral Learning**: revisita tópicos com profundidade crescente
- **Prerequisite Graphs**: DAG de dependências entre conceitos
- **Learning Objectives**: mensuráveis, alinhados a Bloom's taxonomy

### Exercise Generation
- **Procedural**: templates parametrizados → infinitas variações
- **Difficulty Calibration**: IRT (Item Response Theory), adaptive
- **Solution Verification**: execução, property testing, formal proof

### Evaluation Framework
- **Rubrics**: critérios claros, níveis de proficiência
- **Automated Grading**: AST comparison, semantic equivalence, property tests
- **Progress Tracking**: knowledge tracing (BKT/DKT), mastery learning

### Knowledge Distillation
- **Expert → Student**: teacher forcing, logits matching, progressive distillation
- **Model Compression**: quantization (GPTQ, AWQ), pruning, distillation
- **Specialization**: domain-specific fine-tuning (code, math, reasoning)

### Interactive Teaching
- **Socratic Dialogue**: perguntas guiadas, não respostas diretas
- **Worked Examples**: faded guidance (full → partial → independent)
- **Adaptive Feedback**: misconception detection, targeted hints

---

## Roadmap Visual

```
2024-2025          2025-2026           2026-2027           2027+
├─ Fase 6          ├─ Fase 7           ├─ Fase 8           ├─ Fase 9
│  Arch/Eng        │  Specialized      │  Frontier         │  AI Training
│  (6 meses)       │  Domains          │  (contínuo)       │  Síntese
│                  │  (paralelo)       │                   │
│  • ADRs          │  • Systems        │  • AI Coding      │  • Curriculum
│  • DDD/CQRS      │  • Graphics       │  • WASM Comp.     │  • Exercises
│  • Observability │  • Crypto         │  • Effects        │  • Evaluation
│  • GitOps        │  • ML Systems     │  • Quantum        │  • Distillation
│  • Debt Mgmt     │  • Formal Methods │  • New Languages  │  • Teaching
```

---

## Critérios de Prontidão por Fase

| Fase | Gate de Entrada |
|------|-----------------|
| **6** | Fases 1-5 completas + 3+ projetos capstone intermediários |
| **7** | Fase 6 estável + especialização escolhida |
| **8** | Acompanhamento contínuo de papers/conferências (PLDI, POPL, OSDI, SOSP) |
| **9** | Expertise em múltiplos domínios + experiência de ensino/mentoria |

---

*Próximo: [Manutenção](maintenance.md) | [Workflow de Skills](../skills/workflow.md)*