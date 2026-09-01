# Changelog — Kill Front-End (kit)

## v3.1
- DUAS CAMADAS DE VERDADE: o Figma passa a ser a verdade absoluta do ESTADO
  DE REPOUSO (camada 1, pixel-diff ≤1%); estados de interação viram camada 2
  — declarados, não desenhados. Regra não-negociável reescrita na
  orquestradora e no protocols.md.
- Cadeia de precedência por estado: Figma desenhado → declaração
  (docs/interactions.md) → banco de regras → analogia com PRECEDENTE CITADO
  → bloqueio/pergunta ao humano. Analogia sem precedente citável é chute e
  bloqueia — o "nunca inventar valor" continua intacto.
- `interactions-global.md`: banco de regras de interação do kit (I1–I15 +
  famílias de componentes), herdado por todo produto novo; a retro promove
  regras locais genéricas de volta pro kit.
- `templates/interactions.md`: declaração por produto (variants, estados,
  motion, regras locais, decisões inferidas, exceções desenhadas no Figma).
- `templates/components-registry.json` + `scripts/kfe-interactions.mjs`
  (precedent · audit · pending · summary): o registro vivo que dá memória à
  IA — cada lote grava o que decidiu e o componente seguinte herda, com
  auditoria de divergência de regra dentro da família.
- Golden por estado (`tests/golden/states/`): hover/focus/disabled/loading
  ganham regressão medida no QA, aprovada uma vez pelo humano.
- fw-mcp/checklist: variante desenhada deixa de ser exigência — passa a ser
  exigida a linha de declaração. fw-doc grava o registro por lote; fw-onboard
  minera as interações do código existente (B/C nascem com memória);
  fw-github promove regras e mede a evolução das origens na retro.

## v3.0
- REBRAND: o framework agora se chama Kill Front-End (KFE). Skill
  orquestradora `kill-front-end`, comandos /kfe-*, estado em
  docs/kfe-state.md, dashboard kfe-dashboard.mjs, CI kfe-guardian.
- Rumo a produto: o kit passa a ser refinado para operação comercial —
  venda como serviço para empresas (kill-back-end virá na sequência,
  nascendo do contrato OpenAPI + testes E2E que o KFE já entrega).

## v2.5
- Paralelização com subagentes na fw-ui (até 4, verificação central única).
- CI guardião: templates/ci-kfe.yml instalado pela fw-install —
  lint, tipos, build e golden bloqueando merge.
- Relatório de lote pro cliente: scripts/lote-report.mjs (números + lado a
  lado a partir de metrics.md e dos pares de screenshot).
- Calibração global do kit (calibration-global.md): produtos novos herdam;
  a retro promove regras genéricas de volta — aprendizado composto.

## v2.4
- Painel visual gamificado (scripts/kfe-dashboard.mjs + /kfe-dashboard):
  jornada das etapas ao vivo, missão atual, conquistas, lotes e log —
  100% automático (lê kfe-state.md e metrics.md; zero manutenção).

## v2.3
- Kit agnóstico de empresa/projeto (removidas amarras à Alumy; back-end
  definido por quem implementa, com Laravel como default do operador).
- Modo new-ds: design system como entrega (cliente novo — DS primeiro,
  telas depois via new-screens sobre cenário B por construção).
- GUIA.md: passo a passo por cenário com papéis (você · IA · gate).

## v2.2
- Repositório-pronto: install.sh, .gitignore, histórico git iniciado.
- Fontes como pré-requisito da piloto (templates/fonts-checklist.md +
  checagem anti-fallback obrigatória antes de todo diff).
- Golden screen: piloto congelada como regressão do pipeline (tests/golden/),
  rodada no início de lote, em mudança de tokens/deps e em toda release.
- Métricas: docs/metrics.md por lote e por ciclo — o caminho pra trocar o
  "~40%" estimado por número medido.

## v2.1
- templates/ com esqueleto de todos os artefatos docs/ (estado, calibração,
  checklist Figma, auditoria, handoff, QA/release, ADR) — formato nunca mais
  é inventado na hora.
- scripts/pixel-diff.js: verificação objetiva (PASS/FAIL, % de pixels,
  geometria zero-tolerância) usada pela fw-ui e pela tela piloto.
- /kfe-loop: execução contínua que para apenas em gate humano,
  bloqueio ou fim de ciclo.
- Estado com tabela de lotes (new-screens) e trilha AUDIT/ONBOARD (B/C).

## v2
- Cenários A/B/C + fw-audit e fw-onboard · protocolo pixel-perfect na fw-ui
- protocols.md comum (pré-voo, definição de pronto, falha, gate, idempotência)

## v1
- Orquestradora + 9 skills de etapa + 4 comandos.
