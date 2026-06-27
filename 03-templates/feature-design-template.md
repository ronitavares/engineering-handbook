# Feature Design — <Nome da funcionalidade>

**Status:** Draft | Review | Approved | Done  
**Owner:** <Nome / time>  
**Data:** YYYY-MM-DD  
**Produto:** <produto>  
**Links:** PRD, issue, Figma, épico, ADRs relacionados

---

## 1. Contexto do problema

**Responsável:** Produto

Descreva o problema, motivação e contexto.

---

## 2. Objetivos

**Responsável:** Produto

- Objetivo 1
- Objetivo 2

### Métricas esperadas

- Métrica:
- Baseline:
- Alvo:

---

## 3. Escopo

**Responsável:** Produto + Engenharia

### Incluído

- 

### Fora do escopo

- 

---

## 4. Usuários / Personas impactadas

**Responsável:** Produto

| Persona | Impacto |
|---|---|
|  |  |

---

## 5. UX / Handoff

**Responsável:** Design

Links:

- Figma:
- Protótipo:
- Design system:

### Critérios de UX

- Estados de loading:
- Estados de erro:
- Estados vazios:
- Responsividade:
- Acessibilidade:

---

## 6. Functional Design

**Responsável:** Produto + Engenharia

### Regras de negócio

1. 
2. 

### Fluxo principal

1. 
2. 
3. 

### Fluxos alternativos

- 

### Estados funcionais

| Estado | Descrição | Transições |
|---|---|---|
|  |  |  |

### Permissões / papéis

| Ação | Permissão | Papel |
|---|---|---|
|  |  |  |

---

## 7. Technical Design

**Responsável:** Arquitetura + Engenharia

### Contextos / módulos impactados

- 

### APIs / contratos

- Endpoint / Evento / Schema:
- Tipo de mudança: breaking | non-breaking
- Versionamento:

### Dados / persistência

- Tabelas / coleções:
- Migrações:
- Índices:

### Integrações

| Sistema | Direção | Contrato | Observação |
|---|---|---|---|
|  |  |  |  |

### Segurança

- Autenticação:
- Autorização:
- Dados sensíveis:
- Auditoria:

### Observabilidade

- Logs:
- Métricas:
- Tracing:
- Alertas:

### Performance / Resiliência

- SLA esperado:
- Cache:
- Retry:
- Idempotência:
- Degradação:

### Decisões técnicas

| Decisão | Alternativas | Consequência | Precisa de ADR? |
|---|---|---|---|
|  |  |  | Sim/Não |

---

## 8. Critérios de aceite

**Responsável:** Produto + QA

Use formato Given/When/Then quando útil.

- Dado ..., quando ..., então ...

---

## 9. Estratégia de testes

**Responsável:** QA + Engenharia

- Unitários:
- Integração:
- E2E:
- Contrato:
- Regressão:
- Segurança:

---

## 10. Estratégia de rollout

**Responsável:** Engenharia + Produto

- Feature flag:
- Migração:
- Backward compatibility:
- Rollback:
- Monitoramento:

---

## 11. Riscos e mitigação

**Responsável:** Arquitetura + Engenharia

| Risco | Impacto | Probabilidade | Mitigação |
|---|---|---|---|
|  |  |  |  |

---

## 12. Execution Plan

**Responsável:** Engenharia

| Ordem | Tarefa | Validação | Dependência |
|---|---|---|---|
| 1 |  |  |  |

---

## 13. Knowledge Consolidation

**Responsável:** Engenharia + Arquitetura

Após implementação:

- [ ] Feature Design pode ser removida.
- [ ] ADR criado, se necessário.
- [ ] Guidelines atualizadas, se necessário.
- [ ] PRD atualizado, se necessário.
- [ ] Contratos atualizados, se necessário.
- [ ] Artefatos transitórios removidos.

---

## 14. Aprovações

| Área | Responsável | Status | Data |
|---|---|---|---|
| Produto |  | Pending |  |
| Design |  | Pending |  |
| Engenharia |  | Pending |  |
| Arquitetura |  | Pending |  |
| QA |  | Pending |  |
