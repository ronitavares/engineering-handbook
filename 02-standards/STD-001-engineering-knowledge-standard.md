# STD-001 — Engineering Knowledge Standard (EKS)

**Status:** Proposed  
**Versão:** 2.0  
**Owner:** Engenharia / Arquitetura  
**Tipo:** Standard

---

## 1. Objetivo

Definir como **Knowledge Assets** são criados, classificados, consumidos, promovidos e removidos.

O EKS não governa documentação. Ele governa conhecimento.

---

## 2. Knowledge Asset

Um **Knowledge Asset** é qualquer artefato que carrega conhecimento útil para executar, validar, operar ou evoluir software.

Todo Knowledge Asset deve ter:

| Campo | Obrigatório? | Descrição |
|---|---:|---|
| Owner | Sim | Pessoa ou time responsável. |
| Purpose | Sim | Por que existe. |
| Source of truth | Sim | Qual conhecimento governa. |
| Consumers | Sim | Quem usa: pessoas, IA, QA, produto, operação. |
| Lifecycle | Sim | Permanente, transitório ou descartável. |
| Promotion rule | Sim | Quando vira ADR, Guideline, PRD, contrato ou template. |
| Deletion rule | Sim | Quando deve ser removido. |

---

## 3. Fontes oficiais de verdade

| Conhecimento | Fonte oficial |
|---|---|
| Implementação | Código |
| Comportamento esperado | Testes |
| Produto | PRD |
| Arquitetura | ADR |
| Convenções | Guidelines |
| Contratos públicos | OpenAPI, AsyncAPI, schemas ou equivalente |
| Contexto ativo de feature | Feature Design |
| Planejamento temporário | Execution Plan |

Nenhum conhecimento deve ter duas fontes oficiais concorrentes.

---

## 4. Categorias

### 4.1 Durable Knowledge Assets

Permanecem no repositório.

- Código.
- Testes.
- ADR.
- Guidelines.
- Contratos públicos.
- Templates reutilizáveis.
- IaC.
- Scripts de migração.

### 4.2 Product Knowledge Assets

Vivem preferencialmente fora do repositório.

- PRD.
- Roadmap.
- Personas.
- UX handoff.
- Métricas.
- Pesquisa de produto.

### 4.3 Workspace Knowledge Assets

Existem durante a entrega.

- Feature Design.
- Execution Plan.
- Checklist temporário.
- Diagrama exploratório.
- RFC em discussão.

Devem ser removidos após merge, salvo promoção explícita.

### 4.4 Knowledge Exhaust

Resíduo sem valor durável.

- Prompts soltos.
- Conversas com IA.
- Scratchpads.
- Notas pessoais.
- Tentativas abandonadas.

Devem ser descartados.

---

## 5. Knowledge Debt

Knowledge Debt é a dívida gerada quando o conhecimento necessário para operar ou evoluir o sistema não está registrado na fonte correta.

Exemplos:

| Dívida | Correção |
|---|---|
| Decisão arquitetural em chat | Criar ADR |
| Regra crítica sem teste | Criar teste |
| API alterada sem contrato | Atualizar contrato |
| Padrão repetido sem guideline | Criar guideline |
| Feature Design antiga no repo | Remover |
| PRD divergente | Atualizar PRD |
| Contexto duplicado | Eleger fonte única |

Knowledge Debt deve ser tratada como dívida técnica.

---

## 6. Artifact Decision Tree

```text
Tenho uma informação nova
  ├─ É comportamento implementado? → Código + Testes
  ├─ É regra de produto? → PRD
  ├─ É decisão arquitetural? → ADR
  ├─ É contrato de integração? → OpenAPI / AsyncAPI / Schema
  ├─ É padrão reutilizável? → Guideline / Template
  ├─ Só serve para esta entrega? → Feature Design / Execution Plan
  └─ Não terá valor depois? → Delete
```

---

## 7. Política do repositório

O repositório deve conter conhecimento durável e de alta densidade.

### Permitido

- Código e testes.
- ADRs.
- Guidelines.
- Contratos.
- Templates.
- Diagramas estáveis.
- Documentação operacional estável.

### Não permitido como permanente

- Feature Design encerrada.
- Execution Plan encerrado.
- Prompts.
- Conversas com IA.
- Scratchpads.
- Diagramas temporários.
- Documentação que replica implementação.

---

## 8. Knowledge Consolidation

Obrigatória antes do merge.

Perguntas:

1. Alguma decisão precisa virar ADR?
2. Algum padrão precisa virar Guideline?
3. Alguma regra de produto precisa atualizar PRD?
4. Algum contrato mudou?
5. Algum template reutilizável surgiu?
6. Quais artefatos devem ser removidos?

Resultado esperado:

- conhecimento permanente promovido;
- conhecimento transitório removido;
- fonte de verdade atualizada;
- nenhuma decisão relevante perdida em chat/prompt.

---

## 9. AI Readability

Todo Knowledge Asset permanente deve ser legível por agentes de IA.

Isso exige:

- títulos explícitos;
- owner claro;
- escopo declarado;
- linguagem objetiva;
- ausência de duplicação;
- links para fontes oficiais;
- decisão ou regra facilmente extraível.

---

## 10. Maturity indicators

Um time está evoluindo quando:

- reduz specs antigas no repositório;
- aumenta cobertura de testes para regras críticas;
- cria ADRs apenas para decisões permanentes;
- mantém guidelines curtas e acionáveis;
- remove artefatos transitórios regularmente;
- agentes de IA usam contexto correto com menos correção humana.

---

## 11. Regra de ouro

> Se o artefato não é durável, não é fonte oficial e não reduz ambiguidade futura, ele deve ser removido.
