# RFC-002 — Operational Workflow Standard

**Status:** Proposed  
**Versão:** 1.0  
**Owner:** Engenharia  
**Base operacional:** TLC Spec-Driven Development adaptado

---

## 1. Objetivo

Definir o workflow operacional para desenvolvimento de funcionalidades com apoio de IA.

A organização adota o **TLC Spec-Driven Development** como referência operacional, com uma adaptação terminológica: o artefato produzido na fase de Specify será chamado internamente de **Feature Design**.

---

## 2. Workflow oficial

```text
Discovery
  → Feature Design
  → Planning
  → Implementation
  → Validation
  → Knowledge Consolidation
```

A etapa de **Knowledge Consolidation** é uma extensão organizacional obrigatória.

---

## 3. Fase 1 — Discovery

### Objetivo

Compreender o problema de negócio, escopo inicial, usuários impactados, métricas e restrições.

### Responsáveis

- Primário: Produto.
- Participantes: Design, Arquitetura, Engenharia.

### Entrada

- Problema de negócio.
- Métricas ou dor observada.
- Feedback de usuários.
- Demandas regulatórias ou operacionais.

### Saída

- PRD, issue de produto ou briefing aprovado.

### Observação

Discovery normalmente vive fora do repositório.

---

## 4. Fase 2 — Feature Design

### Objetivo

Transformar o problema em uma solução implementável, combinando Functional Design e Technical Design no mesmo artefato.

### Responsáveis

- Functional Design: Produto + Engenharia.
- UX: Design.
- Technical Design: Arquitetura + Engenharia.
- Critérios de aceite: Produto + QA.

### Saída

- Feature Design ativa, usando [`feature-design-template.md`](../03-templates/feature-design-template.md).

### Regras

A Feature Design deve explicar intenção, decisões e restrições. Não deve descrever controllers, services, repositories ou fluxo interno de implementação.

---

## 5. Fase 3 — Planning

### Objetivo

Transformar a Feature Design em plano de execução.

### Responsáveis

- Primário: Engenharia.
- Participantes: IA, QA, Arquitetura.

### Saída

- Jira/GitHub Issues.
- Execution Plan quando necessário.
- Estratégia de testes.
- Estratégia de rollout.

### Regras

O plano deve quebrar a entrega em tarefas pequenas, verificáveis e reversíveis sempre que possível.

---

## 6. Fase 4 — Implementation

### Objetivo

Implementar a solução com código e testes.

### Responsáveis

- Primário: Engenharia.
- Apoio: IA.

### Fonte de verdade

Durante esta fase, o código e os testes passam gradualmente a substituir a Feature Design como fonte mais confiável da implementação.

### Regras

- IA pode propor código, mas engenharia valida.
- Código deve seguir guidelines existentes.
- Decisões arquiteturais não previstas devem ser explicitadas e avaliadas.
- Alterações de contrato devem ser versionadas.

---

## 7. Fase 5 — Validation

### Objetivo

Validar qualidade, comportamento, arquitetura e segurança.

### Responsáveis

- Primário: Engenharia + QA.
- Participantes: Arquitetura, IA.

### Validações mínimas

- Testes automatizados.
- Critérios de aceite.
- Lint/typecheck/build.
- Segurança básica.
- Observabilidade quando aplicável.
- Compatibilidade de contratos.
- Regressão relevante.

---

## 8. Fase 6 — Knowledge Consolidation

### Objetivo

Classificar todo conhecimento produzido durante a feature.

### Responsáveis

- Primário: Engenharia.
- Participantes: Arquitetura, Produto, QA.

### Perguntas obrigatórias

1. Alguma decisão permanente deve virar ADR?
2. Algum padrão reutilizável deve virar Guideline?
3. Alguma regra de negócio mudou e exige atualização do PRD?
4. Algum contrato público mudou?
5. Quais artefatos transitórios devem ser removidos?

### Saída

- ADR criado, se necessário.
- Guidelines atualizadas, se necessário.
- PRD atualizado, se necessário.
- Contratos atualizados, se necessário.
- Artefatos transitórios removidos.

---

## 9. Complexidade e profundidade

Nem toda feature exige a mesma profundidade.

| Tipo de mudança | Feature Design | Execution Plan | ADR |
|---|---:|---:|---:|
| Bug simples | Opcional | Opcional | Não |
| Feature pequena | Sim | Opcional | Raro |
| Feature média | Sim | Sim | Se houver decisão permanente |
| Feature grande | Sim | Sim | Provável |
| Mudança arquitetural | Sim | Sim | Obrigatório |
| Novo serviço | Sim | Sim | Obrigatório |
| Mudança regulatória | Sim | Sim | Possível |

---

## 10. Regras para agentes de IA

Agentes devem consultar informações nesta ordem:

1. Código.
2. Testes.
3. Guidelines.
4. ADRs.
5. Contratos públicos.
6. Feature Design ativa.
7. PRD quando contexto de produto for necessário.

Agentes não devem tratar Feature Design concluída como fonte de verdade.

---

## 11. Definition of Done operacional

Uma entrega só está pronta quando:

- implementação concluída;
- testes passam;
- validação concluída;
- critérios de aceite atendidos;
- Knowledge Consolidation executada;
- artefatos transitórios removidos ou promovidos.

---

## 12. Relação com outros documentos

- [`STD-001`](../02-standards/STD-001-engineering-knowledge-standard.md) define governança do conhecimento.
- [`STD-002`](../02-standards/STD-002-feature-design-standard.md) define estrutura da Feature Design.
- [`RFC-004`](./RFC-004-ai-collaboration-standard.md) define colaboração humano + IA.
