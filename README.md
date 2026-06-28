# AI Engineering Handbook

Este repositório define o **AI Engineering Framework (AEF)**: um framework para desenvolvimento de software assistido por IA, orientado por **Knowledge Assets**, não por acúmulo de documentação.

A decisão central é simples:

> O repositório deve armazenar conhecimento organizacional durável, não o histórico transitório do desenvolvimento.

---

## Estrutura conceitual

O handbook passa a ser organizado em três camadas:

```text
AI Engineering Handbook
│
├── Framework
│   ├── Principles
│   ├── Context Engineering
│   ├── Knowledge Assets
│   ├── Workflow
│   └── Standards
│
├── Engineering References
│   ├── Backend
│   ├── Platform
│   ├── Testing
│   ├── CI/CD
│   ├── Security
│   └── AI-assisted Remediation
│
└── Templates
    ├── Feature Design
    ├── Execution Plan
    ├── ADR
    ├── Guideline
    └── Knowledge Consolidation
```

A camada **Framework** responde “como pensamos”.  
A camada **Engineering References** responde “como fazemos em uma stack específica”.  
A camada **Templates** fornece artefatos operacionais reutilizáveis.

---

## Estrutura do repositório

```text
engineering-handbook/
├── README.md
├── engineering-principles.md
├── context-engineering.md
├── 01-rfcs/
│   └── RFC-001-ai-engineering-framework.md
├── 02-standards/
│   ├── STD-001-engineering-knowledge-standard.md
│   └── STD-002-feature-design-standard.md
├── 03-templates/
│   ├── feature-design-template.md
│   ├── execution-plan-template.md
│   ├── adr-template.md
│   ├── guideline-template.md
│   └── knowledge-consolidation-checklist.md
├── 04-diagrams/
│   ├── framework-overview.mmd
│   ├── operational-workflow.mmd
│   ├── knowledge-lifecycle.mmd
│   ├── artifact-lifecycle.mmd
│   ├── artifact-decision-tree.mmd
│   └── responsibility-matrix.mmd
├── 05-reference/
│   └── backend/
│       ├── README.md
│       ├── nx-bounded-context-monorepo.md
│       ├── validation-gates.md
│       ├── testing-strategy.md
│       ├── ci-cd-release.md
│       ├── governance-security-observability.md
│       ├── documentation-knowledge.md
│       └── ai-assisted-remediation.md
└── glossary.md
```

---

## Documentos principais

| Documento | Objetivo |
|---|---|
| [Engineering Principles](./engineering-principles.md) | Princípios curtos e memoráveis do framework. |
| [RFC-001 — AI Engineering Framework](./01-rfcs/RFC-001-ai-engineering-framework.md) | Visão consolidada do framework, workflow, papéis, artefatos e IA. |
| [STD-001 — Engineering Knowledge Standard](./02-standards/STD-001-engineering-knowledge-standard.md) | Governança de Knowledge Assets, ciclo de vida e política do repositório. |
| [STD-002 — Feature Design Standard](./02-standards/STD-002-feature-design-standard.md) | Padrão da Feature Design, com Functional Design e Technical Design proporcionais à complexidade. |
| [Context Engineering](./context-engineering.md) | Como montar, priorizar e reduzir contexto para agentes de IA. |
| [Backend Reference](./05-reference/backend/README.md) | Referência operacional para Nx + NestJS + TypeORM em monorepo orientado por bounded contexts. |

---

## Workflow operacional

O workflow operacional continua baseado em **TLC Spec-Driven Development**, com uma adaptação interna:

- O termo externo é **Spec-Driven**.
- O artefato interno é **Feature Design**.

```text
Discovery
  → Feature Design
  → Planning
  → Implementation
  → Validation
  → Knowledge Consolidation
```

A etapa final, **Knowledge Consolidation**, é obrigatória.

---

## Workflow adaptativo

| Tipo de mudança | Processo mínimo |
|---|---|
| Bug simples | Código + testes |
| Pequena feature | Feature Design simplificada + testes |
| Feature média | Feature Design completa + Execution Plan |
| Feature grande | Processo completo + rollout + risks |
| Mudança arquitetural | Processo completo + ADR obrigatório |
| Novo serviço/plataforma | Processo completo + ADR + contratos + operação |

---

## Artifact Decision Tree

```text
Nova informação
  ├─ muda produto? → PRD
  ├─ muda arquitetura? → ADR
  ├─ muda contrato? → OpenAPI / AsyncAPI / Schema
  ├─ será reutilizada? → Guideline / Template
  ├─ só serve para a feature atual? → Feature Design / Execution Plan
  └─ terminou a feature? → Delete
```

---

## Regra de ouro

> O código explica **como**. Os Knowledge Assets explicam **por quê**, **para quê** e **sob quais restrições**.

Tudo que apenas replica a implementação deve ser removido ou evitado.
