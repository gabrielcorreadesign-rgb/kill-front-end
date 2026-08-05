---
name: fw-github
description: Etapa 9 do Kill Front-End — GITHUB. Entrega de bastão — organiza o repo, monta o pacote de entrega (contrato + mocks + docs + testes), prepara o handoff pro back e roda a retro do framework. Use quando o orquestrador indicar a etapa 9, ou quando o usuário pedir para fechar/entregar um produto do framework.
---

# Etapa 9 — GITHUB

O bastão é o contrato + o repo — não uma call de duas horas. Se o dev de
back precisar perguntar o básico, a entrega falhou.

## Pré-voo
QA com checklist verde e assinado; contrato OpenAPI fiel aos mocks (audite antes de empacotar — divergência aqui é a pior herança possível pro back).

## Processo

1. **G1 · Repo como produto**: README de onboarding (rodar em 5 minutos:
   clone → install → dev), convenções de branch/commit, histórico limpo.
2. **G2 · Pacote de entrega**: confira dentro do repo: `docs/api-contract.yaml`
   completo e fiel aos mocks · mocks espelhando o contrato · `docs/` viva
   (PRD, regras, specs, ADRs) · `tests/e2e/` · skills do projeto.
3. **G3 · Doc de handoff**: gere `docs/handoff-backend.md` (a partir de
   `templates/handoff-backend.md`) — a tabela
   mock → endpoint: cada rota do contrato, o mock que a simula hoje, a regra
   de negócio associada e o teste E2E que valida. É o mapa do território.
4. **G4 · Protocolo de integração**: registre no handoff: a troca é
   endpoint a endpoint; o mock só morre quando o endpoint real passa nos
   MESMOS testes E2E. O front não refatora — muda a origem do dado.
5. **G5 · Retro do framework**: conduza com o humano (15 min): o que travou?
   o que foi corrigido 2x? qual etapa demorou mais que devia? Converta cada
   resposta em item de `docs/kfe-retro.md` com destino (qual skill/
   hook/regra melhora). Este arquivo alimenta a próxima versão do framework. Revise o
   docs/calibration.md do produto: toda regra que vale pra QUALQUER produto
   (não específica deste Figma) é promovida ao `calibration-global.md` do
   kit — aprendizado composto entre projetos. Consolide também o
   bloco "Por ciclo" de `docs/metrics.md` — é o que substitui o "~40%"
   estimado por um número medido, seu.

## Modo new-ds
O pacote muda: em vez de handoff de back, entrega-se o DS instalável —
repo com tokens + componentes + showcase + doc de uso (como consumir,
como estender, checklist Figma do cliente) + guia de contribuição. A retro
continua obrigatória.

## Definição de pronto (artefatos)

- Repo entregue: README + pacote completo + `docs/handoff-backend.md`
- `docs/kfe-retro.md` com o backlog de melhorias

## Gate (humano — final)

O humano confere o pacote, agenda a sessão de handoff com o dev de back e
declara a entrega. O kfe-state marca o ciclo como concluído.

## Regras

- Todo projeto termina alimentando o framework: retro não é opcional.
- Back-end é implementação manual do time de back — o framework entrega
  tudo PRONTO pra isso, e para aí.

Protocolos comuns: `.claude/skills/kill-front-end/protocols.md`.
