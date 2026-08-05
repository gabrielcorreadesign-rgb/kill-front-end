---
name: kill-front-end
description: Orquestrador do Kill Front-End (v2.3) — agnóstico de empresa e projeto: conduz a construção de qualquer produto com IA, do início à entrega de bastão, em 3 cenários de entrada (produto novo · existente com design system · existente sem/with DS incerto) e 3 modos de produção (new-product, new-screens, new-ds — design system como entrega). Use SEMPRE que o usuário pedir para iniciar um produto ou um design system, onboardar um produto existente, criar telas novas, continuar o fluxo (/kfe-next) ou consultar estado (/kfe-status). Esta skill roteia; nunca execute uma etapa sem passar por aqui.
---

# Kill Front-End — Orquestrador (v2)

Você conduz o fluxo. As skills de etapa executam. O humano é o orquestrador:
decide nos gates; você executa entre eles.
Protocolos comuns (pré-voo, definição de pronto, falha, idempotência):
`.claude/skills/kill-front-end/protocols.md` — leia uma vez por sessão.

## Cenários de entrada (C0 — sempre o primeiro passo)

Antes de qualquer etapa, classifique o produto:

| Cenário | Situação | Rota |
|---|---|---|
| **A · Produto novo** | Nada existe | Pipeline completo: etapas 1→9 |
| **B · Existe, COM design system** | Código e/ou Figma têm DS reconhecível | `fw-audit` → `fw-onboard` (pareamento) → modo `new-screens` |
| **C · Existe, SEM DS (ou incerto)** | Estilo ad-hoc, tokens soltos, paridade desconhecida | `fw-audit` → `fw-onboard` (engenharia reversa) → modo `new-screens` |

Se o usuário não sabe o cenário: rode `fw-audit` — o diagnóstico dela
classifica com evidências e o humano confirma. NUNCA assuma B sem auditar:
"tem um DS" costuma significar C.

## Modos de produção

| Modo | Pipeline | Entrega |
|---|---|---|
| `new-product` | 1→9 | Produto completo (front + contrato pro back) |
| `new-screens` | 5-lite→9 por lote | Telas novas em produto onboardado |
| `new-ds` | 1,2,3,4 → 5 (direção) → 6 (só fundações+componentes) → 7 → 9 | Design system como produto: tokens + componentes pareados + doc + showcase — telas ficam pra um ciclo new-screens futuro |

`new-ds` serve a entrega "design system primeiro, telas depois" (comum em
cliente novo): o QA (8) reduz-se à golden screen + a11y dos componentes, e o
GITHUB (9) entrega o DS documentado no lugar do handoff de back.

## Protocolo de estado (`docs/kfe-state.md`)

Crie a partir do template do kit: `templates/kfe-state.md` (cenário A
usa a tabela 1–9; B/C usa AUDIT/ONBOARD + 5–9; new-screens registra lotes).
Resumo do formato:

```md
# Kill Front-End — estado
Produto: <nome> · Cenário: <A|B|C> · Modo: <new-product|new-screens>
Kit: v2 · Início: <data> · Baseline de fidelidade: <—|N,N% (tela piloto)>

| # | Etapa | Status | Gate | Aprovado em |
|---|-------|--------|------|-------------|
(A: etapas 1–9 · B/C: AUDIT, ONBOARD e depois 5→9 por lote)

## Exceções aprovadas
- <data> · <o quê> · <por quem>

## Log
- <data> · <evento>
```

Status: `pendente` · `em-andamento` · `aguardando-gate` · `concluída` ·
`bloqueada(<motivo>)`.

## O loop

`/kfe-next` avança um passo. `/kfe-loop` roda contínuo e para
somente em gate humano, bloqueio ou fim do ciclo. Em ambos:

1. Leia o estado. Não existe → volte ao C0.
2. Identifique a primeira etapa não-concluída; rode o PRÉ-VOO dela
   (protocols.md). Pré-voo falhou → status `bloqueada`, reporte, PARE.
3. Execute o processo da skill da etapa.
4. Confira a DEFINIÇÃO DE PRONTO da etapa (artefatos + checagens). Incompleta
   → continue ou reporte com o protocolo de falha.
5. Completa → `aguardando-gate`; apresente o resumo de gate (formato no
   protocols.md).
6. Aprovação explícita do humano → `concluída` + log. Em loop autorizado,
   siga direto e pare apenas nos gates humanos.

## Regras não-negociáveis (herdadas por todas as skills)

- NUNCA pule gate humano, mesmo com autorização de loop contínuo.
- NUNCA marque etapa concluída sem a definição de pronto batida.
- NUNCA invente valor: dado que não veio do Figma (via MCP), do código ou do
  humano não entra no produto. Sem o dado → pergunte ou releia; jamais estime.
- Nenhum código de produto antes do INSTALL (cenário A) ou do ONBOARD (B/C).
- O Figma é a verdade absoluta; divergência visual é bug do código.
- Humano decide, IA executa: escopo, fluxo e UX de interação são sempre
  opções apresentadas, nunca decisões silenciosas.
- Repetiu 2x → proponha registrar em skill/CLAUDE.md/calibration antes de
  continuar.
- Back-end nunca é implementado: entrega-se contrato + mocks + handoff.

## Templates e scripts do kit

Todo artefato docs/ tem esqueleto em `templates/` — SEMPRE crie a partir
dele (nunca invente formato). Verificação de fidelidade:
`scripts/pixel-diff.js` (requer `npm i -D pixelmatch pngjs` no produto).
Painel visual: `scripts/kfe-dashboard.mjs` (comando
/kfe-dashboard) — lê o estado e as métricas, zero manutenção.
