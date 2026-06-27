# Context Engineering

**Status:** Proposed  
**Versão:** 2.0  
**Owner:** Engenharia / Arquitetura

---

## 1. Objetivo

Definir como selecionar, priorizar e montar contexto para agentes de IA.

Context Engineering é a disciplina de fornecer ao agente o menor conjunto de informações capaz de produzir a melhor decisão ou implementação.

> Mais contexto não significa melhor contexto.

---

## 2. Problema

Agentes de IA podem falhar quando recebem:

- documentação antiga;
- specs encerradas;
- PRDs extensos sem foco;
- decisões contraditórias;
- prompts com baixa precisão;
- código insuficiente;
- excesso de contexto irrelevante.

Isso gera **context drift**: o agente opera sobre uma representação incorreta do sistema.

---

## 3. Hierarquia de contexto

Use esta ordem para montar contexto técnico:

1. Código relevante.
2. Testes relevantes.
3. Contratos públicos.
4. Guidelines.
5. ADRs.
6. Feature Design ativa.
7. PRD ou contexto de produto, apenas se necessário.

Nunca priorize documentação antiga sobre código e testes.

---

## 4. Context Assembly

Ao pedir trabalho para IA, forneça:

| Bloco | Conteúdo |
|---|---|
| Objetivo | O que precisa ser feito. |
| Escopo | O que pode ser alterado. |
| Restrições | O que não pode ser quebrado. |
| Fontes | Arquivos, testes, ADRs e contratos relevantes. |
| Validação | Como provar que funcionou. |
| Saída esperada | Código, plano, revisão ou análise. |

---

## 5. Context Budget

Contexto deve ser tratado como orçamento.

Antes de adicionar um documento ao contexto, pergunte:

1. Ele contém conhecimento não inferível pelo código?
2. Ele está atualizado?
3. Ele é necessário para esta tarefa?
4. Ele reduz ambiguidade?
5. Ele pode confundir o agente?

Se a resposta for incerta, prefira código, testes e contratos.

---

## 6. Context Drift

Context Drift ocorre quando o agente usa contexto que não representa mais o sistema.

Exemplos:

- Feature Design antiga usada após merge.
- PRD divergente do comportamento implementado.
- ADR superado por decisão nova não registrada.
- README desatualizado.
- Prompt reutilizado fora do contexto original.

Mitigação:

- remover artefatos transitórios;
- versionar contratos;
- criar ADRs para decisões permanentes;
- manter guidelines curtas;
- consultar código e testes primeiro.

---

## 7. Knowledge Drift

Knowledge Drift é a divergência entre conhecimento organizacional e realidade operacional.

É mais amplo que Context Drift.

Exemplos:

- time acredita que uma regra existe, mas ela não está testada;
- guideline antiga orienta padrão que não é mais usado;
- decisão arquitetural vive apenas em conversa;
- PRD descreve produto desejado, mas não produto entregue.

Mitigação:

- Knowledge Consolidation obrigatória;
- owners explícitos;
- revisão periódica de ADRs e guidelines;
- remoção agressiva de artefatos temporários.

---

## 8. Prompt mínimo recomendado

```text
Objetivo:
<o que deve ser feito>

Contexto prioritário:
- Código: <arquivos>
- Testes: <arquivos>
- ADR/Guideline: <links>

Restrições:
- <restrição 1>
- <restrição 2>

Validação:
- <comando/teste/critério>

Saída esperada:
- <plano/código/revisão>
```

---

## 9. Regra de ouro

> O melhor contexto é o menor conjunto de informações corretas, relevantes e verificáveis para a tarefa.
