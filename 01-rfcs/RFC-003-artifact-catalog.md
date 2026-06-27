# RFC-003 — Artifact Catalog

**Status:** Proposed  
**Versão:** 1.0  
**Owner:** Engenharia / Arquitetura

---

## 1. Objetivo

Definir o catálogo oficial de artefatos do AI Engineering Framework, sua finalidade, dono, fonte de verdade e ciclo de vida.

Todo artefato criado durante o desenvolvimento deve pertencer a uma categoria oficial e possuir destino definido.

---

## 2. Categorias oficiais

| Categoria | Finalidade | Persistência |
|---|---|---|
| Knowledge Assets | Conhecimento durável da organização. | Permanente |
| Knowledge Inputs | Entradas de produto, negócio ou contexto. | Externo / enquanto vigente |
| Knowledge Workspace | Artefatos usados durante a execução. | Transitório |
| Knowledge Outputs | Saídas permanentes geradas após consolidação. | Permanente |
| Knowledge Exhaust | Resíduos de trabalho sem valor durável. | Descartável |

---

## 3. Knowledge Assets

Conhecimento durável, confiável e útil para evolução futura.

| Artefato | Objetivo | Owner | Local |
|---|---|---|---|
| Código | Implementação do sistema. | Engenharia | Repositório |
| Testes | Comportamento esperado e regressão. | Engenharia / QA | Repositório |
| ADR | Decisões arquiteturais permanentes. | Arquitetura | Repositório |
| Guidelines | Convenções reutilizáveis. | Engenharia | Repositório |
| Contratos públicos | APIs, eventos e schemas. | Engenharia / Arquitetura | Repositório |
| Templates | Modelos reutilizáveis. | Engenharia | Repositório |
| IaC | Infraestrutura declarativa. | Engenharia / Plataforma | Repositório |

---

## 4. Knowledge Inputs

Entradas que orientam o desenvolvimento, mas não necessariamente pertencem ao repositório.

| Artefato | Objetivo | Owner | Local recomendado |
|---|---|---|---|
| PRD | Problema, objetivo, escopo e métricas. | Produto | Notion / Confluence |
| Roadmap | Planejamento de produto. | Produto | Ferramenta de produto |
| UX/UI Handoff | Fluxos, telas e critérios de UX. | Design | Figma / ferramenta de design |
| Benchmark | Pesquisa e referências. | Produto / Design | Wiki / Notion |
| Pesquisa técnica | Exploração antes da decisão. | Engenharia | Wiki / temporário |

---

## 5. Knowledge Workspace

Artefatos temporários criados para reduzir incerteza durante a execução.

| Artefato | Objetivo | Owner | Destino |
|---|---|---|---|
| Feature Design | Definir solução funcional e técnica. | Produto + Engenharia | Remover ou promover partes |
| Execution Plan | Quebrar a execução em tarefas. | Engenharia | Remover |
| Checklist temporário | Controlar validações específicas. | Engenharia / QA | Remover |
| Diagrama exploratório | Apoiar raciocínio de solução. | Engenharia | Remover ou promover |
| RFC em discussão | Coletar feedback antes de decisão. | Autor da RFC | Remover ou converter em ADR |

---

## 6. Knowledge Outputs

Saídas permanentes resultantes da Knowledge Consolidation.

| Artefato | Quando gerar |
|---|---|
| ADR | Houve decisão arquitetural permanente. |
| Guideline | Surgiu padrão reutilizável. |
| PRD atualizado | Mudou comportamento de produto. |
| Contrato atualizado | API, evento ou schema mudou. |
| Template | Um artefato transitório tornou-se reutilizável. |

---

## 7. Knowledge Exhaust

Resíduos operacionais que não devem permanecer.

| Artefato | Política |
|---|---|
| Prompts | Não versionar como fonte permanente. |
| Conversas com IA | Não versionar como fonte permanente. |
| Scratchpads | Remover. |
| Notas pessoais | Remover ou migrar para artefato oficial. |
| Logs manuais de tentativa | Remover. |
| Planos obsoletos | Remover. |

---

## 8. Matriz de ciclo de vida

| Artefato | Nasce em | Morre em | Pode virar |
|---|---|---|---|
| PRD | Discovery | Quando produto muda | PRD atualizado |
| Feature Design | Feature Design | Merge | ADR, Guideline, PRD |
| Execution Plan | Planning | Merge | — |
| Código | Implementation | Refatoração/depreciação | — |
| Testes | Implementation | Mudança de comportamento | — |
| ADR | Knowledge Consolidation | Nunca | Novo ADR substitutivo |
| Guideline | Knowledge Consolidation | Revisão de padrão | Guideline atualizada |
| Prompt | Qualquer fase | Fim da tarefa | Template, raramente |

---

## 9. Regras de criação

Todo artefato deve declarar:

- objetivo;
- owner;
- status;
- ciclo de vida;
- destino esperado;
- fonte de verdade relacionada.

Artefatos sem owner ou destino devem ser removidos.

---

## 10. Regras de permanência

Um artefato só permanece no repositório se:

1. é durável;
2. possui owner;
3. não duplica o código;
4. é fonte oficial de algum conhecimento;
5. será útil para humanos ou IA no futuro.

---

## 11. Anti-padrões

Evitar:

- pasta `docs/specs` acumulando specs antigas;
- documentos que explicam implementação já entregue;
- múltiplas versões divergentes de design;
- diagramas não atualizados;
- README duplicando OpenAPI;
- prompt salvo como decisão técnica.

---

## 12. Relação com Knowledge Consolidation

A Knowledge Consolidation deve classificar cada artefato criado durante a feature segundo este catálogo.

Nenhum artefato transitório deve sobreviver sem promoção explícita.
