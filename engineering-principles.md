# Engineering Principles

**Status:** Active  
**Versão:** 2.0  
**Owner:** Engenharia

---

## 1. Code is the implementation truth

O código é a fonte da verdade sobre como o sistema funciona em produção.

Não documente fluxos internos que podem ser inferidos pelo código.

---

## 2. Tests are the behavioral truth

Testes documentam o comportamento esperado.

Se uma regra é crítica, ela deve ser testável.

---

## 3. Knowledge must outlive implementation

Conhecimento durável explica decisões, restrições e trade-offs.

Artefatos que apenas ajudaram na execução devem desaparecer.

---

## 4. Optimize for AI readability

O repositório deve ser legível para pessoas e agentes de IA.

Isso significa:

- alta densidade de contexto;
- fontes claras de verdade;
- pouca duplicação;
- baixo drift.

---

## 5. Every artifact has a lifecycle

Todo artefato precisa ter:

- owner;
- propósito;
- fonte de verdade relacionada;
- regra de promoção;
- regra de remoção.

---

## 6. Humans own decisions

IA pode analisar, sugerir, escrever e revisar.

Humanos decidem escopo, arquitetura, segurança, compliance e promoção de conhecimento.

---

## 7. Prefer adaptive rigor

O processo deve ser proporcional ao risco.

Bugs simples não precisam do mesmo rigor que mudanças arquiteturais.

---

## 8. Minimize knowledge drift

Drift é dívida.

Se um artefato tende a divergir do código, ele deve ser temporário ou substituído por teste, contrato, ADR ou guideline.

---

## 9. Context is an engineering asset

O contexto entregue a agentes de IA deve ser selecionado, priorizado e reduzido.

Mais contexto nem sempre melhora o resultado.

---

## 10. Delete is a valid outcome

Remover artefatos transitórios é parte do processo.

Nem toda informação merece sobreviver ao merge.
