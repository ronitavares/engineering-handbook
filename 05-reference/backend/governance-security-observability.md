# Governance, Security & Observability

## Objetivo

Definir controles transversais para manter o backend seguro, observável, auditável e com ownership claro.

---

## Segurança

### Secrets

Regras:

- nunca commitar secrets;
- `.env.example` contém apenas nomes de variáveis;
- secrets vêm do ambiente ou secret manager;
- scans de secrets devem rodar em CI e, quando possível, pre-commit.

### Dependency e code scanning

CI deve executar, conforme maturidade:

- dependency audit;
- SAST;
- container scanning;
- license compliance;
- secret scanning.

---

## AuthN vs AuthZ

Separar autenticação técnica de autorização de negócio.

```text
libs/security
  → valida JWT/API key/HMAC/mTLS
  → extrai tenant/contexto técnico
  → provê guards/decorators técnicos

domain policy
  → decide regra de negócio
  → valida permissões comerciais
  → aplica restrições funcionais
```

Exemplo:

```text
libs/security valida o token.
domain policy decide se o seller pode cancelar o pedido.
```

---

## Observabilidade

Padrões mínimos:

- structured logs;
- correlation/request id;
- tracing entre runtimes e mensagens;
- métricas de latência, erro e throughput;
- health checks;
- readiness/liveness;
- redaction de PII/secrets.

---

## Ownership

Cada projeto deve ter owner.

```text
/domains/catalog/          @org/catalog-team
/apps/apis/catalog-api/    @org/catalog-team
/libs/contracts/           @org/platform-team
/libs/kernel/              @org/platform-team
```

Regras:

- ownership alinha com `scope:*`;
- `contracts` e `kernel` têm alto blast radius;
- mudanças em libs cross-cutting exigem review de platform/architecture;
- exceções viram ADR.

---

## Governance process

Decisões significativas viram ADR.

Criar ADR quando:

- criar/splitar/mergear bounded context;
- alterar matriz de dependência;
- mudar estratégia de persistência;
- introduzir lib cross-cutting;
- criar exceção de boundary;
- mudar estratégia de autenticação/autorização;
- alterar processo de release/deploy;
- assumir risco operacional relevante.

---

## Branch protection

Checks recomendados:

- format;
- lint;
- unit;
- build;
- integration/contract/e2e quando aplicável;
- migration check;
- secret scan;
- dependency scan;
- code scan;
- owner review.

---

## Operational Knowledge Assets

Mudanças operacionais podem gerar Knowledge Assets permanentes:

| Mudança | Knowledge Asset |
|---|---|
| Novo runtime | runbook |
| Novo fluxo de deploy | release guide |
| Novo risco operacional | ADR |
| Novo alarme | observability guideline |
| Novo padrão de autenticação | security guideline |
| Nova exceção | ADR |

---

## Checklist

- [ ] Secrets não foram commitados.
- [ ] PII/secrets não são logados.
- [ ] Auth técnica está em `libs/security`.
- [ ] Regra de autorização de negócio está no domínio.
- [ ] Logs possuem correlation id.
- [ ] Runtime possui health/readiness/liveness quando aplicável.
- [ ] Projeto possui owner.
- [ ] Mudança em `contracts/kernel` teve review adequado.
- [ ] Exceções foram registradas em ADR.
