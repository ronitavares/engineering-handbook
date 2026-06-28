# Testing Strategy

## Objetivo

Definir como organizar testes em um backend Nx + NestJS + TypeORM usando bounded contexts.

A estratégia prioriza confiança no menor custo possível e separa claramente testes de unidade, integração, contrato e e2e.

---

## Pirâmide recomendada

| Nível | Volume | Foco | Local | Target |
|---|---:|---|---|---|
| Unit | 70–80% | Domínio, use cases, policies, value objects, mappers | co-locado em `domains/*` / `libs/*` | `test` |
| Integration | ~15% | DB real, repositories, adapters, migrations | `tests/integration/<context>` | `integration` |
| Contract | baixo | Acordos entre producer/consumer | `tests/contracts/<producer>-<consumer>` | `contract` |
| E2E | 5–10% | Fluxos críticos fim a fim | `tests/e2e/<api>` | `e2e` |

---

## Regras estruturais

```text
apps/             contém runtimes deployáveis.
tests/            contém suites executáveis.
libs/test-support contém suporte reutilizável para testes.
```

Não criar:

```text
apps/<runtime>-e2e
domains/<context>/e2e
libs/testing
```

---

## Unit tests

Devem ser co-locados ao código testado.

```text
domains/catalog/src/product/core/use-case/create-product.use-case.spec.ts
```

Regras:

- sem DB;
- sem rede;
- sem containers;
- mockar I/O;
- focar regra de negócio;
- fixtures internas ficam próximas ao spec.

---

## Integration tests

Vivem em projetos próprios.

```text
tests/integration/<context-or-capability>/
```

Validam:

- repositories;
- mapping de persistência;
- constraints reais;
- adapters;
- migrations;
- context module contra DB real.

---

## Contract tests

Vivem em:

```text
tests/contracts/<producer>-<consumer>/
```

Validam:

- DTOs públicos;
- eventos;
- schemas;
- compatibilidade producer/consumer;
- versionamento.

Contract tests reduzem necessidade de e2e cross-runtime pesado.

---

## E2E tests

Vivem em:

```text
tests/e2e/<api>/
tests/e2e/cross-runtime/
```

E2E é obrigatório para fluxos importantes.

Deve cobrir:

- sucesso;
- validação;
- autenticação/autorização;
- conflitos;
- not found;
- idempotência quando aplicável;
- side effects persistidos.

Evitar e2e que valida apenas status code happy path.

---

## Test support

```text
libs/test-support/
├── containers/
├── database/
├── http/
├── matchers/
├── random/
├── factories/<context>/
└── builders/<context>/
```

Regras:

- factories/builders constroem apenas shapes públicos;
- podem importar `@org/contracts` e `@org/kernel`;
- não importam domains, apps, entities ou repositories;
- production code nunca importa test-support.

---

## AI-assisted testing

Ao gerar testes, agentes devem seguir a sequência:

```text
1. Ler critérios de aceite.
2. Identificar comportamento crítico.
3. Escolher o menor nível de teste que dá confiança.
4. Gerar unit tests para regra pura.
5. Gerar integration para I/O real.
6. Gerar contract para fronteiras públicas.
7. Gerar e2e para fluxo importante.
8. Rodar gates afetados.
```

---

## Definition of Done de testes

- [ ] Regras críticas possuem unit tests.
- [ ] I/O real possui integration test.
- [ ] Contratos públicos possuem contract test quando há consumer relevante.
- [ ] Fluxos importantes possuem e2e com sucesso e edge cases.
- [ ] Factories/builders não violam boundaries.
- [ ] `nx affected -t test integration contract e2e` passa conforme aplicável.
