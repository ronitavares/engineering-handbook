# Backend Reference Library

Esta pasta contém referências operacionais para aplicar o AI Engineering Framework em uma stack específica:

> **Nx + NestJS + TypeScript + TypeORM + pnpm**

A referência não substitui o framework. Ela traduz os princípios do AEF para decisões práticas de arquitetura, estrutura, validação, CI/CD, governança e correção assistida por IA.

---

## Relação com o Framework

| Camada | Pergunta que responde |
|---|---|
| AEF / RFC-001 | Como pensamos engenharia assistida por IA? |
| EKS / STD-001 | Como governamos Knowledge Assets? |
| FDS / STD-002 | Como desenhamos features? |
| Backend Reference | Como aplicamos isso em Nx + NestJS + TypeORM? |

---

## Documentos

| Documento | Objetivo |
|---|---|
| [Nx Bounded Context Monorepo](./nx-bounded-context-monorepo.md) | Estrutura de referência para backend em monorepo Nx com bounded contexts. |
| [Validation Gates](./validation-gates.md) | Gates mínimos para build, lint, testes, arquitetura, migração e release. |
| [Testing Strategy](./testing-strategy.md) | Estratégia de testes por nível: unit, integration, contract e e2e. |
| [CI/CD & Release](./ci-cd-release.md) | Pipeline, affected builds, versionamento, deploy e rollback. |
| [Governance, Security & Observability](./governance-security-observability.md) | Segurança, ownership, observabilidade e regras de governança. |
| [Documentation & Knowledge](./documentation-knowledge.md) | Como conhecimento técnico específico da stack vira Knowledge Asset. |
| [AI-assisted Remediation](./ai-assisted-remediation.md) | Como corrigir violações com apoio de agentes de IA. |

---

## Como usar

Use esta referência quando a Feature Design indicar impacto em backend, arquitetura, persistência, testes, CI/CD ou runtime.

Fluxo recomendado:

```text
Feature Design
  → identificar impacto técnico
  → consultar Backend Reference relevante
  → montar contexto para IA
  → implementar
  → validar gates
  → executar Knowledge Consolidation
```

---

## Escopo

Esta referência é prescritiva para projetos que adotam:

- Nx monorepo;
- NestJS;
- TypeScript;
- TypeORM;
- pnpm;
- bounded contexts;
- APIs/workers como runtimes;
- contracts/kernel/infrastructure/security/observability como libs técnicas;
- testes separados em `tests/`;
- validação via `nx affected`.

Para outras stacks, mantenha os princípios e substitua os comandos/layouts por referências específicas.
