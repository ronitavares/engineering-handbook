# STD-002 — Feature Design Standard (FDS)

**Status:** Proposed  
**Versão:** 1.0  
**Owner:** Produto + Engenharia + Arquitetura  
**Tipo:** Standard

---

## 1. Objetivo

Definir a estrutura oficial da **Feature Design**, o principal artefato colaborativo usado durante o desenvolvimento de funcionalidades.

A Feature Design combina dois níveis de design no mesmo artefato:

1. **Functional Design** — o que será construído, por quê, para quem e com quais critérios.
2. **Technical Design** — como a solução será integrada ao sistema, quais decisões técnicas existem e quais impactos devem ser tratados.

---

## 2. Natureza do artefato

A Feature Design é um artefato **transitório**.

Ela vive durante o desenvolvimento da feature e deve ser removida após a entrega, salvo quando algum conhecimento for promovido para ADR, Guideline, PRD ou contrato público.

---

## 3. O que a Feature Design deve fazer

Ela deve reduzir incerteza antes da implementação.

Deve responder:

- qual problema estamos resolvendo;
- qual resultado esperado;
- qual escopo;
- quais regras de negócio;
- quais critérios de aceite;
- quais fluxos de UX são relevantes;
- quais decisões técnicas importam;
- quais integrações/contratos serão afetados;
- quais riscos existem;
- como validar e fazer rollout.

---

## 4. O que a Feature Design não deve fazer

Não deve descrever detalhes inferíveis pelo código.

Evitar:

- sequência Controller → Service → Repository;
- nomes de classes que ainda podem mudar;
- pseudo-código equivalente à implementação;
- cópia de endpoints já descritos em OpenAPI;
- documentação de fluxo interno de métodos;
- diagramas sincronizados manualmente com código.

---

## 5. Responsabilidades por seção

| Seção | Responsável primário | Participantes |
|---|---|---|
| Contexto do problema | Produto | Engenharia, Design |
| Objetivos | Produto | Engenharia |
| Escopo e fora do escopo | Produto | Engenharia, Arquitetura |
| UX / Fluxos | Design | Produto, Engenharia |
| Critérios de aceite | Produto + QA | Engenharia |
| Functional Design | Produto + Engenharia | QA, Design |
| Technical Design | Arquitetura + Engenharia | IA |
| Estratégia de testes | QA + Engenharia | IA |
| Rollout | Engenharia | Produto, Operações |
| Riscos | Arquitetura + Engenharia | Produto, QA |
| Knowledge Consolidation | Engenharia | Arquitetura, Produto |

Ninguém é dono isolado da Feature Design inteira. Cada disciplina é dona da sua parte.

---

## 6. Estrutura oficial

Uma Feature Design deve conter:

1. Metadados.
2. Contexto.
3. Objetivos.
4. Não objetivos.
5. Escopo.
6. Personas/usuários impactados.
7. UX / Handoff.
8. Functional Design.
9. Technical Design.
10. Critérios de aceite.
11. Estratégia de testes.
12. Estratégia de rollout.
13. Riscos e mitigação.
14. Plano de execução.
15. Knowledge Consolidation.
16. Aprovações.

O template oficial está em [`feature-design-template.md`](../03-templates/feature-design-template.md).

---

## 7. Functional Design

### Deve conter

- Regras de negócio.
- Estados funcionais relevantes.
- Permissões e papéis quando aplicável.
- Fluxos principais.
- Fluxos alternativos.
- Mensagens, erros e exceções relevantes.
- Critérios de aceite em linguagem verificável.

### Não deve conter

- Implementação interna.
- Estrutura de banco.
- Classes e métodos.
- Detalhes de framework.

---

## 8. Technical Design

### Deve conter, quando aplicável

- Contextos/domínios afetados.
- Contratos de API/eventos.
- Mudanças em banco de dados.
- Integrações externas.
- Decisões arquiteturais.
- Segurança.
- Observabilidade.
- Performance.
- Resiliência.
- Compatibilidade e versionamento.
- Estratégia de migração.

### Não deve conter

- Pseudo-código extenso.
- Descrição de serviços triviais.
- Duplicação do código esperado.
- Listagem mecânica de arquivos a alterar, salvo no plano de execução.

---

## 9. Nível de profundidade

A profundidade deve ser proporcional à complexidade.

| Complexidade | Expectativa |
|---|---|
| Pequena | Functional Design curto, Technical Design mínimo. |
| Média | Functional Design completo e Technical Design objetivo. |
| Grande | Functional + Technical completos, riscos, rollout e validação detalhados. |
| Arquitetural | Technical Design completo e provável ADR. |

---

## 10. Critérios de qualidade

Uma boa Feature Design é:

- clara;
- verificável;
- objetiva;
- de alta densidade;
- útil para humanos e IA;
- sem duplicação da implementação;
- rastreável até critérios de aceite;
- descartável após a entrega.

---

## 11. Sinais de problema

A Feature Design deve ser revisada se:

- parece um tutorial de código;
- copia endpoints ou DTOs inteiros sem necessidade;
- não deixa claro o objetivo da feature;
- não possui critérios de aceite;
- não identifica responsáveis;
- não define riscos;
- não pode ser usada por QA para validar;
- não pode ser usada por Engenharia para planejar.

---

## 12. Aprovação

A aprovação mínima depende da complexidade:

| Tipo | Aprovação mínima |
|---|---|
| Pequena | Engenharia |
| Média | Produto + Engenharia |
| Grande | Produto + Engenharia + Arquitetura + QA |
| Arquitetural | Arquitetura + Engenharia |
| Regulatória | Produto + Jurídico/Compliance + Engenharia |

---

## 13. Encerramento

Ao final da feature, a Feature Design deve passar pela Knowledge Consolidation.

Possíveis destinos:

- remover;
- extrair ADR;
- atualizar Guideline;
- atualizar PRD;
- atualizar contrato.

A Feature Design não deve permanecer como documentação permanente da implementação.
