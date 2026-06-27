# STD-002 — Feature Design Standard (FDS)

**Status:** Proposed  
**Versão:** 2.0  
**Owner:** Produto + Engenharia + Arquitetura  
**Tipo:** Standard

---

## 1. Objetivo

Definir a **Feature Design** como um canvas colaborativo e transitório para reduzir incerteza antes da implementação.

A Feature Design combina:

- **Functional Design**: problema, objetivo, escopo, regras, UX e critérios.
- **Technical Design**: arquitetura, dados, contratos, segurança, testes e rollout.
- **Knowledge Decisions**: o que deve virar ADR, Guideline, PRD, contrato ou ser deletado.

---

## 2. Natureza

Feature Design não é documentação permanente.

Ela existe enquanto a feature está sendo construída. Após merge, deve ser removida ou ter partes promovidas.

---

## 3. Canvas oficial

```text
FEATURE DESIGN CANVAS

Business
  Problem | Users | Goals | Scope | Non-goals | Acceptance

Experience
  UX flows | States | Errors | Accessibility | Handoff

Engineering
  Architecture | Data | Contracts | Security | Observability | Risks

Delivery
  Tests | Rollout | Migration | Dependencies | Execution Plan

Knowledge
  ADR? | Guideline? | PRD update? | Contract update? | Delete?
```

O template oficial está em [`feature-design-template.md`](../03-templates/feature-design-template.md).

---

## 4. Responsáveis por seção

| Bloco | Responsável primário | Participantes |
|---|---|---|
| Business | Produto | Engenharia, Design |
| Experience | Design | Produto, Engenharia |
| Engineering | Arquitetura + Engenharia | IA |
| Delivery | Engenharia + QA | Produto, Operações |
| Knowledge | Engenharia + Arquitetura | Produto, QA |

---

## 5. Níveis de profundidade

| Nível | Quando usar | O que preencher |
|---|---|---|
| Light | Bug, ajuste pequeno, baixa incerteza | Objetivo, escopo, aceites e validação |
| Standard | Feature média ou integração simples | Canvas completo, mas objetivo |
| Full | Feature grande, alto risco ou múltiplos times | Canvas completo + rollout + riscos + ADR provável |
| Architecture | Mudança estrutural | Technical Design completo + ADR obrigatório |

---

## 6. Quando criar Feature Design

Criar quando houver pelo menos um item:

- mais de uma interpretação possível;
- regra de negócio nova;
- impacto em contrato;
- impacto em UX;
- risco técnico;
- integração externa;
- mudança em dados;
- necessidade de alinhamento entre áreas;
- agente de IA precisará de contexto estruturado.

Não criar para bugs triviais ou mudanças totalmente localizadas com teste claro.

---

## 7. Quando omitir seções

| Seção | Pode omitir quando |
|---|---|
| UX | Não há impacto de experiência. |
| Technical Design | Mudança é local e inferível pelo código. |
| Rollout | Sem feature flag, migração ou risco operacional. |
| Data | Não muda persistência. |
| Contracts | Não muda API/evento/schema. |
| Risks | Risco é baixo e explícito. |

Omitir é aceitável. Deixar seção vazia sem justificativa não é.

---

## 8. O que não deve entrar

Evitar:

- sequência Controller → Service → Repository;
- pseudo-código extenso;
- nomes de classes ainda instáveis;
- documentação duplicada da OpenAPI;
- diagramas que precisam acompanhar cada refactor;
- logs de conversa com IA;
- plano detalhado demais para tarefas triviais.

---

## 9. Critérios de qualidade

Uma boa Feature Design:

- reduz incerteza;
- define responsáveis;
- possui critérios verificáveis;
- tem densidade alta;
- é proporcional à complexidade;
- é útil para IA sem virar fonte permanente;
- facilita planejamento e validação;
- é deletável após a entrega.

---

## 10. Feature Design como contexto para IA

A Feature Design deve ser escrita para humanos e agentes.

Boas práticas:

- frases curtas;
- decisões explícitas;
- constraints visíveis;
- links para fontes oficiais;
- evitar ambiguidade;
- separar fatos de hipóteses;
- destacar validação esperada.

---

## 11. Encerramento

Antes do merge, responder:

1. Alguma decisão virou ADR?
2. Algum padrão virou Guideline?
3. Alguma regra atualizou PRD?
4. Algum contrato mudou?
5. A Feature Design pode ser deletada?

A resposta padrão esperada é: **deletar**.
