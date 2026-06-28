# AI-assisted Remediation

## Objetivo

Definir como violações de arquitetura, qualidade, testes, CI/CD, segurança ou documentação devem ser corrigidas com apoio de agentes de IA.

A premissa é:

> Humanos decidem e revisam. A IA aplica a menor correção possível e valida.

---

## Fluxo de correção

```text
Detectar violação
  → classificar área + regra
  → montar contexto mínimo
  → delegar correção ao agente
  → aplicar menor diff possível
  → rodar gates afetados
  → revisão humana
  → Knowledge Consolidation quando necessário
```

---

## Prompt padrão de correção

```text
Contexto:
Você está trabalhando em um monorepo Nx + NestJS + TypeORM.
Siga o AI Engineering Handbook e a Backend Reference Library.

Violação:
<descrever regra violada>

Arquivos/projetos afetados:
<listar caminhos>

Estado esperado:
<descrever a forma correta>

Restrições:
- Faça a menor alteração possível.
- Não crie pastas proibidas.
- Não enfraqueça boundaries.
- Não altere escopo não relacionado.
- Não deixe decisão permanente apenas no chat.

Validação:
Rode ou liste os gates necessários:
- nx affected -t build lint:check test integration contract e2e
- migration:show se houver persistência
- format:check

Saída esperada:
- resumo da correção;
- diff conceitual;
- gates executados;
- conhecimento que deve ser promovido, se houver.
```

---

## Catálogo de correções

| Violação | Correção |
|---|---|
| App com regra de negócio | Mover regra para domínio/capability. |
| Domain importando app | Inverter dependência; app compõe domain. |
| Client app importando domain | Substituir por contracts + HTTP. |
| Entity vazando em response | Criar DTO/mapper e remover export. |
| Direct domain-to-domain import | Usar contracts/eventos/app composition/ports. |
| Migration em app/capability | Mover para infrastructure/persistence/migrations do contexto. |
| Entity alterada sem migration | Gerar e revisar migration. |
| Teste unitário acessando DB | Mover para integration ou mockar I/O. |
| Suite e2e dentro de app | Mover para `tests/e2e/<api>`. |
| Prompt salvo como doc permanente | Remover ou transformar em template/guideline. |
| Decisão sem ADR | Criar ADR. |
| Guideline desatualizada | Atualizar ou remover. |
| Contrato quebrado sem versão | Restaurar contrato antigo e criar nova versão. |

---

## Correções estruturais

Mudanças estruturais devem preferir:

- Nx generators;
- codemods;
- renames consistentes;
- updates de aliases;
- updates de tags;
- updates de boundaries;
- updates de implicitDependencies.

Evitar mover arquivos manualmente sem atualizar o grafo.

---

## Correções de Knowledge Debt

Knowledge Debt ocorre quando conhecimento importante não está em fonte confiável.

| Sintoma | Correção |
|---|---|
| Decisão importante só no chat | ADR |
| Regra crítica sem teste | Teste |
| Padrão repetido informalmente | Guideline |
| Contrato implícito | Schema/OpenAPI/AsyncAPI |
| Feature Design antiga ainda usada | Remover ou arquivar fora do repo |
| README divergente | Atualizar ou remover |

---

## Guardrails para IA

Agente não deve:

- inventar arquitetura;
- criar abstrações sem necessidade;
- adicionar interfaces “por precaução”;
- enfraquecer lint/boundaries;
- remover testes para fazer pipeline passar;
- ignorar migrations;
- alterar contrato público silenciosamente;
- expandir escopo da tarefa.

---

## Definition of Done da correção

- [ ] Violação foi corrigida.
- [ ] Diff é mínimo.
- [ ] Gates aplicáveis passam ou foram explicitamente reportados.
- [ ] Nenhuma nova violação foi introduzida.
- [ ] Decisões permanentes foram promovidas.
- [ ] Artefatos transitórios foram removidos.
