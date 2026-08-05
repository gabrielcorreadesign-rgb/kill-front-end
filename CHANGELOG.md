# Changelog — Framework de IA (kit)

## v2.5
- Paralelização com subagentes na fw-ui (até 4, verificação central única).
- CI guardião: templates/ci-framework.yml instalado pela fw-install —
  lint, tipos, build e golden bloqueando merge.
- Relatório de lote pro cliente: scripts/lote-report.mjs (números + lado a
  lado a partir de metrics.md e dos pares de screenshot).
- Calibração global do kit (calibration-global.md): produtos novos herdam;
  a retro promove regras genéricas de volta — aprendizado composto.

## v2.4
- Painel visual gamificado (scripts/framework-dashboard.mjs + /framework-dashboard):
  jornada das etapas ao vivo, missão atual, conquistas, lotes e log —
  100% automático (lê framework-state.md e metrics.md; zero manutenção).

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
- /framework-loop: execução contínua que para apenas em gate humano,
  bloqueio ou fim de ciclo.
- Estado com tabela de lotes (new-screens) e trilha AUDIT/ONBOARD (B/C).

## v2
- Cenários A/B/C + fw-audit e fw-onboard · protocolo pixel-perfect na fw-ui
- protocols.md comum (pré-voo, definição de pronto, falha, gate, idempotência)

## v1
- Orquestradora + 9 skills de etapa + 4 comandos.
