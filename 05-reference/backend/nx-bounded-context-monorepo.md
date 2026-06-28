# Nx Bounded Context Monorepo

## Objetivo

Definir uma referência operacional para backends NestJS + TypeORM em monorepo Nx usando **bounded contexts** como unidade principal de ownership técnico e funcional.

Esta referência existe para transformar princípios do AEF em decisões concretas de estrutura, dependência e validação.

---

## Modelo mental

```text
Monorepo organiza produtos.
Apps executam.
Domains governam negócio.
Capabilities organizam funcionalidades.
Core concentra domínio e aplicação.
HTTP expõe contratos.
Persistence encapsula banco de dados.
Libs compartilham apenas o que é verdadeiramente cross-cutting.
Tests executam suites separadas.
```

---

## Estrutura alvo

```text
apps/
├── apis/<api>/
├── workers/<worker>/
├── frontend/
├── portal/
├── cli/
└── mobile/

domains/<context>/
└── src/
    ├── <context>.module.ts
    ├── <capability>/
    │   ├── core/
    │   ├── http/rest/
    │   ├── persistence/
    │   └── infrastructure/
    ├── commons/
    └── infrastructure/
        └── persistence/migrations/

libs/
├── contracts/
├── kernel/
├── infrastructure/
├── security/
├── observability/
├── ui/
└── test-support/

tests/
├── e2e/
├── integration/
└── contracts/
```

---

## Regras centrais

| Regra | Decisão |
|---|---|
| Apps executam | APIs/workers/client apps vivem em `apps/`. |
| Domains governam negócio | Regras de negócio vivem em `domains/<context>`. |
| Capabilities são pastas | Não criar módulo NestJS por capability por padrão. |
| Um módulo por contexto | `domains/<context>/src/<context>.module.ts`. |
| Libs são cross-cutting | Nenhuma regra de negócio em `libs/*`. |
| Contracts são puros | Sem NestJS, TypeORM, entities ou runtime. |
| Kernel é genérico | Apenas primitivas estáveis e agnósticas. |
| Apps não possuem negócio | Apps compõem módulos e cuidam de runtime. |
| Client apps não importam domains | Usam `@org/contracts` e HTTP. |
| Tests são projetos próprios | Suites executáveis vivem em `tests/`, não em `apps/`. |

---

## Apps

Apps são runtimes deployáveis.

### APIs

```text
apps/apis/<api>/
```

Responsabilidades:

- bootstrap;
- HTTP server;
- Swagger runtime;
- health/metrics;
- configuração;
- composição de módulos de domínio.

Não devem conter:

- regras de negócio;
- entities;
- repositories;
- use cases internos de domínio.

### Workers

```text
apps/workers/<worker>/
```

Responsabilidades:

- filas;
- jobs;
- schedulers;
- consumidores assíncronos;
- composição de domínios.

---

## Domains

Domains são bounded contexts.

```text
domains/<context>/
```

Responsabilidades:

- regras de negócio;
- use cases;
- policies;
- entities;
- repositories concretos;
- migrations do contexto;
- contratos HTTP locais;
- documentação de linguagem ubíqua.

---

## Capabilities

Capabilities organizam uma funcionalidade dentro de um bounded context.

Criar capability quando houver dois ou mais sinais:

- vocabulário próprio;
- endpoint raiz próprio;
- lifecycle independente;
- persistência própria;
- regra de negócio não trivial;
- três ou mais arquivos relacionados;
- ownership distinto.

---

## Public barrels

Cada domínio deve exportar apenas sua superfície pública intencional.

Preferir:

```ts
export { CatalogModule } from './catalog.module';
```

Evitar:

```ts
export * from './product/persistence/entity/product.entity';
export * from './product/persistence/repository/product.repository';
export * from './product/core/use-case/create-product.use-case';
```

---

## Dependency direction

```text
backend apps → domains → libs
client apps  → contracts/kernel/ui → HTTP APIs
domains      → contracts/kernel/infrastructure/security/observability
```

Proibido:

```text
domain → app
client app → domain
kernel → NestJS/TypeORM/domain
contracts → NestJS/TypeORM/domain
production code → test-support/tests
```

---

## Integration / Connect APIs

Uma Connect API é um runtime externo com Anti-Corruption Layer.

```text
External Consumer → Connect API → ACL → Internal Domains
```

Deve viver em:

```text
apps/apis/<channel>-api
```

Não deve virar:

```text
domains/connect
libs/connect
apps/services/connect-service
```

Responsabilidades:

- external contracts;
- authN/authZ do consumidor externo;
- resolução de tenant/ownership;
- tradução externo ↔ interno;
- rate limit;
- idempotência;
- auditoria;
- versionamento público.

Não possui regra de negócio central nem persistência direta.

---

## Tags Nx recomendadas

```text
type:app
type:domain
type:contract
type:kernel
type:infrastructure
type:security
type:observability
type:ui
type:test-support
type:test-suite

platform:server
platform:worker
platform:web
platform:mobile
platform:cli

boundary:integration

test:e2e
test:integration
test:contract

scope:<bounded-context-or-area>
```

---

## Definition of Done estrutural

Uma alteração estrutural só está pronta quando:

- tags Nx estão corretas;
- aliases `@org/*` resolvem;
- boundaries são respeitadas;
- barrel público não vaza internals;
- nenhum app possui regra de negócio;
- nenhum domain importa app;
- nenhuma entity vaza para contracts ou responses;
- gates de validação passam.
