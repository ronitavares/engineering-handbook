# Documentation & Knowledge

## Objetivo

Definir como conhecimento técnico específico da stack backend deve ser capturado, promovido ou removido.

Este documento aplica o Engineering Knowledge Standard ao contexto Nx + NestJS + TypeORM.

---

## Princípio

> Documentação backend deve explicar ownership, decisões, contratos e operação — não duplicar código.

---

## Onde cada conhecimento vive

| Conhecimento | Fonte oficial |
|---|---|
| Implementação | Código |
| Comportamento | Testes |
| Decisão arquitetural | ADR |
| Contrato externo | OpenAPI / AsyncAPI / Schema |
| Regra de negócio | PRD + testes |
| Linguagem de domínio | README do bounded context |
| Operação | Runbook |
| Convenção técnica | Guideline |
| Planejamento temporário | Feature Design / Execution Plan |

---

## READMEs por projeto

Cada bounded context deve ter README curto contendo:

- propósito;
- responsabilidade de negócio;
- capabilities;
- linguagem ubíqua;
- owners;
- contratos públicos;
- notas de schema/migration;
- links para ADRs relevantes.

Cada app/runtime deve ter README curto contendo:

- o que expõe;
- quais domínios compõe;
- env vars relevantes;
- health/metrics;
- como rodar localmente;
- links para runbooks.

---

## ADRs

ADRs são obrigatórios para decisões permanentes.

Exemplos:

- novo bounded context;
- split/merge de contexto;
- nova lib cross-cutting;
- exceção de boundary;
- mudança de persistência;
- estratégia de autenticação;
- estratégia de release;
- integração externa crítica.

---

## Diagramas

Preferir diagramas textuais e versionáveis.

```text
Mermaid
Structurizr
C4 textual
ERD gerado
```

Evitar binários como fonte da verdade.

---

## Feature Design e specs temporárias

Feature Design, Execution Plan, prompts e scratchpads são transitórios.

Após merge:

- remover;
- ou promover trechos para ADR/Guideline/PRD/Contrato;
- nunca manter como documentação permanente da implementação.

---

## Per-context knowledge

Cada contexto deve manter sua linguagem e fronteira explícitas.

Checklist:

- [ ] propósito claro;
- [ ] capabilities listadas;
- [ ] termos de domínio definidos;
- [ ] eventos públicos listados;
- [ ] DTOs/schemas públicos referenciados;
- [ ] owners definidos;
- [ ] ADRs relacionados linkados.

---

## Knowledge Consolidation backend

Antes do merge, responder:

1. Alguma decisão técnica merece ADR?
2. Algum padrão deve virar Guideline?
3. Algum contrato foi alterado?
4. Alguma operação exige Runbook?
5. Algum README precisa ser atualizado?
6. Algum artefato temporário deve ser removido?

---

## Anti-padrões

Evitar:

- README que replica estrutura de arquivos;
- diagrama manual que tenta acompanhar classes;
- spec antiga usada como fonte de verdade;
- ADR editado para esconder mudança de decisão;
- documentação de endpoint que duplica OpenAPI;
- prompt salvo como decisão técnica;
- docs sem owner.

---

## Regra prática

Se a informação muda toda vez que o código muda, ela provavelmente pertence ao código ou aos testes.

Se a informação explica por que a solução existe, ela pode ser um Knowledge Asset durável.
