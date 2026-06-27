# STD-001 — Engineering Knowledge Standard (EKS)

**Status:** Proposed  
**Versão:** 1.0  
**Owner:** Engenharia / Arquitetura  
**Tipo:** Standard

---

## 1. Objetivo

Definir como o conhecimento de engenharia deve ser criado, classificado, armazenado, promovido e descartado.

O EKS responde:

> Como a organização governa conhecimento técnico e organizacional?

Ele não define como implementar features. Essa responsabilidade é do workflow operacional.

---

## 2. Premissa central

> Documentação não é o objetivo. Conhecimento útil é o objetivo.

Todo artefato deve aumentar a capacidade de humanos e agentes de IA compreenderem, decidirem ou evoluírem o sistema.

---

## 3. Fontes oficiais de verdade

| Tipo de conhecimento | Fonte oficial |
|---|---|
| Implementação | Código |
| Comportamento esperado | Testes |
| Produto | PRD |
| Arquitetura | ADR |
| Convenções | Guidelines |
| Contratos públicos | OpenAPI, AsyncAPI, schemas ou documentos equivalentes |
| Definição temporária de feature | Feature Design |
| Planejamento temporário | Execution Plan |

Nenhum conhecimento deve ter duas fontes oficiais.

---

## 4. Categorias de conhecimento

### 4.1 Conhecimento permanente

Conhecimento durável, confiável e útil por longo prazo.

Exemplos:

- código;
- testes;
- ADRs;
- guidelines;
- contratos públicos;
- templates reutilizáveis;
- scripts de migração;
- infraestrutura como código.

Deve permanecer no repositório.

### 4.2 Conhecimento de produto

Conhecimento de negócio, objetivos, escopo e regras funcionais.

Exemplos:

- PRD;
- roadmap;
- personas;
- fluxos de produto;
- métricas;
- decisões de escopo.

Preferencialmente fica fora do repositório, em ferramenta de produto ou wiki corporativa.

### 4.3 Conhecimento transitório

Conhecimento útil apenas durante o desenvolvimento.

Exemplos:

- Feature Design;
- Execution Plan;
- checklists temporários;
- diagramas temporários;
- prompts;
- conversas com IA;
- scratchpads;
- notas de trabalho.

Deve ser removido após a entrega, salvo se promovido.

---

## 5. Política do repositório

### Permitido

- Código.
- Testes.
- ADRs.
- Guidelines.
- Contratos públicos.
- Templates reutilizáveis.
- Documentação operacional estável.
- Diagramas de arquitetura estáveis.

### Não permitido como conteúdo permanente

- Feature Design concluída.
- Execution Plan concluído.
- Brainstorms.
- RFCs em discussão encerradas.
- Prompts e conversas com IA.
- Scratchpads.
- Diagramas temporários.
- Documentação que apenas reproduz o código.

---

## 6. Densidade de conhecimento

Um artefato deve maximizar:

```text
Conhecimento novo / esforço de leitura
```

Artefatos de alta densidade:

- explicam decisões;
- documentam trade-offs;
- reduzem ambiguidade;
- registram restrições relevantes;
- orientam evolução futura.

Artefatos de baixa densidade:

- descrevem controllers;
- repetem o código;
- listam chamadas internas;
- copiam APIs já descritas em contratos;
- envelhecem rapidamente.

Artefatos de baixa densidade devem ser removidos ou reescritos.

---

## 7. Knowledge Consolidation

A Knowledge Consolidation é obrigatória antes de uma feature ser considerada concluída.

Ela responde:

> O que deste trabalho deve permanecer como conhecimento organizacional?

### 7.1 Destinos possíveis

| Destino | Quando usar |
|---|---|
| Descartar | Quando o artefato só serviu para execução. |
| Promover para ADR | Quando houve decisão arquitetural permanente. |
| Promover para Guideline | Quando surgiu prática reutilizável. |
| Atualizar PRD | Quando houve mudança funcional ou de escopo. |
| Atualizar contrato | Quando API, evento ou schema mudou. |
| Manter como template | Quando o artefato virou modelo reutilizável. |

### 7.2 Artefatos normalmente descartados

- Feature Design.
- Execution Plan.
- Prompts.
- Scratchpads.
- Diagramas exploratórios.
- Checklists temporários.

### 7.3 Artefatos normalmente promovidos

- Decisões permanentes → ADR.
- Padrões repetíveis → Guideline.
- Mudanças de produto → PRD.
- Contratos versionados → OpenAPI / AsyncAPI / schema.

---

## 8. ADRs

ADRs registram decisões arquiteturais permanentes.

Um ADR deve conter:

- contexto;
- decisão;
- alternativas consideradas;
- consequências;
- status;
- data;
- responsáveis.

ADRs são históricos. Não devem ser editados para representar estado novo, exceto correções editoriais. Mudança de decisão deve gerar novo ADR.

---

## 9. Guidelines

Guidelines registram convenções aplicáveis a múltiplas features.

Devem ser:

- objetivas;
- prescritivas;
- testáveis quando possível;
- úteis para humanos e agentes de IA.

Guidelines não devem virar tutorial extenso nem replicar documentação pública de frameworks.

---

## 10. Contratos públicos

Contratos são fontes de verdade para integrações.

Exemplos:

- OpenAPI;
- AsyncAPI;
- JSON Schema;
- Protobuf;
- tabelas de eventos versionados;
- contratos SQS/Kafka.

Mudanças de contrato devem seguir política de versionamento.

---

## 11. Critérios para criar artefato

Antes de criar um artefato, responder:

1. O código já responde isso?
2. Os testes já cobrem esse comportamento?
3. Esse conhecimento continuará útil em seis meses?
4. Este artefato reduz ambiguidade real?
5. Este artefato representa decisão, restrição ou contrato?
6. Um agente de IA se beneficiará desta informação sem ser confundido por drift?

Se a maioria das respostas for negativa, o artefato não deve ser criado.

---

## 12. Critérios para remover artefato

Remover quando:

- a feature foi entregue;
- o artefato descreve implementação já inferível pelo código;
- o conteúdo está divergente;
- o artefato não tem owner;
- o artefato não possui ciclo de vida claro;
- o conhecimento relevante já foi promovido.

---

## 13. Regra de ouro

> O repositório deve conter apenas conhecimento durável, de alta densidade e não inferível de forma confiável pelo código.

Tudo que não atende esse critério é transitório.
