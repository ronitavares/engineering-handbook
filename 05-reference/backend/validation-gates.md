# Validation Gates

## Objetivo

Definir os gates mínimos que uma alteração backend deve passar antes de merge.

O gate valida código, arquitetura, contratos, migrações e comportamento. Ele deve ser aplicado igualmente para código humano e código assistido por IA.

---

## Gate padrão

```bash
pnpm exec nx affected -t build lint:check test integration contract e2e migration:show
pnpm exec nx format:check
```

Em mudanças com persistência, incluir também verificação de migrações pendentes.

---

## Gates por tipo

| Mudança | Gate mínimo |
|---|---|
| Bug sem persistência | `build`, `lint:check`, `test` |
| Feature pequena | `build`, `lint:check`, `test`, e2e relevante |
| Feature com I/O | `integration`, `contract` quando aplicável |
| Mudança de API/evento | `contract`, e2e, versionamento |
| Mudança de entity | migration generate/show, integration |
| Mudança de runtime | e2e, health, observability |
| Mudança arquitetural | full gate + ADR |

---

## Checklist estrutural

- [ ] Apps não possuem regras de negócio.
- [ ] Domains não importam apps.
- [ ] Client apps não importam domains.
- [ ] Não há import direto entre bounded contexts sem ADR.
- [ ] Barrels públicos não exportam entities, repositories ou use cases internos.
- [ ] Contracts/kernel continuam puros.
- [ ] Production code não importa `libs/test-support` nem `tests/*`.
- [ ] Nenhuma pasta proibida foi criada (`shared`, `features`, `modules`, `libs/shared`).

---

## Checklist de persistência

- [ ] Entity alterada possui migration.
- [ ] Migration está no contexto correto.
- [ ] Migration possui `up` e `down`.
- [ ] Migration não depende de services/use cases/providers runtime.
- [ ] `synchronize` continua `false`.
- [ ] Operação destrutiva possui rollout ou ADR.
- [ ] `migration:show` passa.

---

## Checklist de contratos

- [ ] Contratos públicos estão versionados.
- [ ] Breaking change possui nova versão.
- [ ] Eventos/DTOs não expõem detalhes internos.
- [ ] `libs/contracts` não depende de NestJS/TypeORM/domains.
- [ ] Consumers impactados foram identificados.

---

## Checklist para IA

- [ ] Agente consultou código/testes antes de docs transitórias.
- [ ] Agente não inventou estrutura.
- [ ] Agente respeitou tags e boundaries.
- [ ] Alteração é mínima e focada.
- [ ] Gates foram executados ou explicitamente listados para execução humana.
- [ ] Decisão permanente não ficou apenas no chat.

---

## Definition of Done

Uma alteração só pode ser considerada pronta quando:

- gate aplicável passa;
- falhas foram corrigidas pela menor mudança possível;
- Knowledge Consolidation foi executada;
- ADR/Guideline/PRD/contratos foram atualizados quando necessário;
- artefatos temporários foram removidos.
