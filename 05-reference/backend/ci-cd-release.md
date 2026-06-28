# CI/CD & Release

## Objetivo

Definir a referência operacional para integração contínua, entrega, versionamento e deploy em backends Nx.

A pipeline deve ser construída sobre o grafo do Nx, usando `affected`, cache e gates proporcionais ao risco.

---

## Pipeline padrão

```text
install
  → format:check
  → lint:check
  → test
  → build
  → integration
  → contract
  → e2e
  → migration:show
  → docker build
  → deploy
  → migration:run
  → smoke test
```

---

## Fast path de PR

Obrigatório para todo PR:

```bash
pnpm install --frozen-lockfile
pnpm exec nx format:check
pnpm exec nx affected -t lint:check test build
```

Para PRs com I/O, contrato, runtime ou fluxo crítico:

```bash
pnpm exec nx affected -t integration contract e2e
pnpm exec nx run-many -t migration:show
```

---

## Regras de affected

CI deve usar:

```text
fetch-depth: 0
nx-set-shas
nx affected
```

Evitar `run-many` em PRs, exceto para checks globais como `migration:show` quando necessário.

---

## Caching

Regras:

- targets determinísticos podem ser cacheáveis;
- `build`, `test`, `lint:check`, `integration`, `contract`, `e2e` podem usar cache se herméticos;
- migrations e deploy nunca são cacheáveis;
- remote cache deve ser habilitado para CI e devs.

---

## Artifacts

| App type | Artifact |
|---|---|
| API | container image |
| Worker | container image |
| Web/Portal | static bundle ou image |
| CLI | npm package ou binário |
| Mobile | store build |

Domains e libs internos não são publicados por padrão.

---

## Versionamento

Recomendação:

```text
independent versioning per app
```

Versionamento deve ser baseado em Conventional Commits.

Exemplo:

```text
catalog-api@1.4.0
payments-worker@2.1.3
```

---

## Deploy

Princípios:

- construir o artifact uma vez;
- promover o mesmo SHA entre ambientes;
- configuração vem do ambiente/secret manager;
- migrations rodam pós-deploy;
- rollback é artifact-first.

```text
build image once
  → dev
  → staging
  → prod
```

---

## Migrations no deploy

Migrations devem rodar:

- depois do novo artifact estar disponível;
- em ordem explícita por contexto;
- com política forward-only em operação normal;
- com expand/contract para mudanças destrutivas.

---

## Rollback

| Área | Estratégia |
|---|---|
| Artifact | redeploy da imagem anterior |
| Schema | forward-fix preferencial |
| Breaking change | evitar via versionamento/compatibilidade |
| Config | reverter env/feature flag |

Rollback de schema só deve ocorrer quando o `down` foi desenhado e validado para isso.

---

## Required checks

Branch protection deve exigir:

- `format:check`;
- `lint:check`;
- `test`;
- `build`;
- `integration` quando aplicável;
- `contract` quando aplicável;
- `e2e` quando aplicável;
- `migration:show`;
- pending migration guard;
- secret/dependency/security scans.

---

## Knowledge Consolidation no release

Antes do release:

- [ ] ADR criado para decisão permanente.
- [ ] Guideline atualizada para padrão reutilizável.
- [ ] PRD atualizado para mudança funcional.
- [ ] Contratos versionados.
- [ ] Runbook atualizado para mudança operacional.
- [ ] Artefatos transitórios removidos.
