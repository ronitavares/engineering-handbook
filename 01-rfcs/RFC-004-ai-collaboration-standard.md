# RFC-004 — AI Collaboration Standard

**Status:** Proposed  
**Versão:** 1.0  
**Owner:** Engenharia

---

## 1. Objetivo

Definir como Produto, Design, Arquitetura, Engenharia, QA e agentes de IA colaboram no ciclo de desenvolvimento.

A IA é uma ferramenta de aceleração e apoio cognitivo. A responsabilidade por decisões, qualidade, segurança e governança do conhecimento permanece humana.

---

## 2. Princípios

1. IA auxilia; humanos decidem.
2. Código gerado por IA deve passar pelos mesmos critérios de qualidade que código humano.
3. IA deve seguir fontes oficiais de verdade.
4. IA não deve tratar artefatos transitórios como permanentes.
5. Toda decisão arquitetural permanente deve ser registrada por humanos em ADR.
6. Toda entrega termina com Knowledge Consolidation.

---

## 3. Papéis humanos

| Papel | Responsabilidades |
|---|---|
| Produto | Problema, objetivos, escopo, regras de negócio, PRD. |
| Design | Experiência, fluxos, handoff, critérios de UX. |
| Arquitetura | Decisões técnicas, trade-offs, coerência sistêmica, ADR. |
| Engenharia | Implementação, testes, plano, validação técnica. |
| QA | Estratégia de testes, critérios de aceite, regressão. |
| Operações/Plataforma | Deploy, observabilidade, infraestrutura e confiabilidade. |

---

## 4. Responsabilidades da IA

A IA pode apoiar:

- análise de contexto;
- geração de hipóteses;
- decomposição de tarefas;
- escrita inicial de Feature Design;
- revisão de critérios de aceite;
- geração de código;
- refatoração;
- geração de testes;
- revisão de segurança básica;
- revisão de documentação;
- preparação de Knowledge Consolidation.

A IA não deve ser a autoridade final sobre:

- escopo de produto;
- decisões regulatórias;
- arquitetura permanente;
- segurança crítica;
- aprovação de release;
- descarte ou promoção de conhecimento organizacional.

---

## 5. Ordem de consulta para IA

Agentes devem consultar informações nesta ordem:

1. Código.
2. Testes.
3. Guidelines.
4. ADRs.
5. Contratos públicos.
6. Feature Design ativa.
7. PRD quando necessário.

Nunca priorizar:

- specs antigas;
- conversas passadas;
- prompts soltos;
- documentos sem owner;
- Feature Design já concluída.

---

## 6. Regras para prompts

Prompts usados em execução devem:

- indicar objetivo;
- informar contexto mínimo;
- apontar fontes oficiais;
- explicitar restrições;
- pedir validação;
- evitar instruções conflitantes.

Prompts não devem permanecer no repositório como documentação permanente, salvo se forem transformados em template ou guideline.

---

## 7. Modo de colaboração por fase

| Fase | Humano | IA |
|---|---|---|
| Discovery | Define problema e escopo | Resume, compara, sugere perguntas |
| Feature Design | Decide solução | Ajuda a estruturar e identificar lacunas |
| Planning | Define estratégia | Quebra tarefas e riscos |
| Implementation | Aprova e integra código | Gera, refatora e explica código |
| Validation | Decide qualidade | Gera testes e revisa falhas |
| Knowledge Consolidation | Decide destino dos artefatos | Sugere promoções e remoções |

---

## 8. Guardrails

IA não deve:

- inventar contratos;
- ignorar testes falhando;
- alterar ADRs sem instrução explícita;
- criar documentação permanente sem motivo;
- substituir decisão de arquitetura;
- remover código sem entender uso;
- modificar segurança sem revisão humana;
- usar documentação transitória como fonte permanente.

---

## 9. Definition of Done com IA

Uma contribuição assistida por IA só está pronta quando:

- o engenheiro revisou o código;
- testes relevantes foram executados;
- mudanças foram explicadas;
- contratos foram atualizados, se necessário;
- riscos foram avaliados;
- artefatos transitórios foram classificados;
- nenhuma decisão permanente ficou apenas no chat ou prompt.

---

## 10. Revisão de código assistida por IA

A IA pode revisar:

- inconsistência com guidelines;
- ausência de testes;
- erros óbvios;
- riscos de segurança;
- complexidade desnecessária;
- duplicação;
- drift com ADRs.

A aprovação final continua sendo humana.

---

## 11. Segurança e compliance

Conteúdo sensível não deve ser inserido em prompts sem autorização.

Evitar compartilhar:

- segredos;
- tokens;
- credenciais;
- dados pessoais;
- dados de clientes;
- informações reguladas.

Quando necessário, mascarar dados.

---

## 12. Métrica de sucesso

O uso de IA deve melhorar:

- lead time;
- qualidade dos testes;
- clareza de design;
- velocidade de revisão;
- consistência arquitetural;
- redução de documentação obsoleta.

Não deve aumentar drift, ambiguidade ou dívida documental.
