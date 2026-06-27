# Engineering Handbook

Este repositório define o **AI Engineering Framework (AEF)**: um conjunto de RFCs, Standards, templates e diagramas para desenvolvimento de software assistido por IA.

O framework combina:

1. **Engineering Knowledge Standard (EKS)** — governança do conhecimento organizacional.
2. **Workflow Operacional baseado em TLC Spec-Driven Development** — execução estruturada de funcionalidades.
3. **AI Collaboration Standard** — regras de colaboração entre pessoas e agentes de IA.

A decisão central do framework é simples:

> O repositório deve armazenar conhecimento organizacional durável, não o histórico transitório do desenvolvimento.

---

## Estrutura

```text
engineering-handbook/
├── README.md
├── 01-rfcs/
│   ├── RFC-001-ai-engineering-framework.md
│   ├── RFC-002-operational-workflow.md
│   ├── RFC-003-artifact-catalog.md
│   └── RFC-004-ai-collaboration-standard.md
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
│   └── responsibility-matrix.mmd
└── glossary.md
```

---

## Documentos principais

| Documento | Objetivo |
|---|---|
| [RFC-001 — AI Engineering Framework](./01-rfcs/RFC-001-ai-engineering-framework.md) | Visão geral do framework, princípios e componentes. |
| [STD-001 — Engineering Knowledge Standard](./02-standards/STD-001-engineering-knowledge-standard.md) | Política de governança do conhecimento, ciclo de vida e repositório. |
| [RFC-002 — Operational Workflow](./01-rfcs/RFC-002-operational-workflow.md) | Workflow operacional baseado em TLC Spec-Driven, adaptado para Feature Design. |
| [STD-002 — Feature Design Standard](./02-standards/STD-002-feature-design-standard.md) | Estrutura oficial da Feature Design, com Functional Design e Technical Design. |
| [RFC-003 — Artifact Catalog](./01-rfcs/RFC-003-artifact-catalog.md) | Catálogo oficial de artefatos e seus ciclos de vida. |
| [RFC-004 — AI Collaboration Standard](./01-rfcs/RFC-004-ai-collaboration-standard.md) | Regras de colaboração entre Produto, Design, Arquitetura, Engenharia, QA e IA. |

---

## Princípios resumidos

1. Código é a fonte da verdade da implementação.
2. Testes são a fonte da verdade do comportamento esperado.
3. ADRs registram decisões permanentes.
4. Feature Design é transitória.
5. O workflow operacional usa TLC Spec-Driven, mas internamente o artefato principal se chama **Feature Design**.
6. Todo artefato deve ter ciclo de vida definido.
7. O processo termina somente após **Knowledge Consolidation**.

---

## Como usar

Para uma nova funcionalidade:

1. Comece pelo PRD ou entrada de produto.
2. Crie uma Feature Design usando o template em `03-templates/feature-design-template.md`.
3. Quebre a execução em um Execution Plan quando necessário.
4. Implemente com código e testes.
5. Valide critérios, arquitetura e segurança.
6. Execute a Knowledge Consolidation.
7. Promova apenas conhecimento durável para ADR, Guidelines ou PRD.
8. Remova os artefatos transitórios.

---

## Regra de ouro

> O código explica **como**. Os artefatos explicam **por quê**, **para quê** e **sob quais restrições**.

Tudo que apenas replica a implementação deve ser removido ou evitado.
