# Changelog — Framework de IA (kit)

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
