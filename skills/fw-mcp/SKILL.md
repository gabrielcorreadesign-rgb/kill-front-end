---
name: fw-mcp
description: Etapa 4 do Kill Front-End (v2) — MCP. Conecta e CALIBRA o ambiente Claude Code + Figma + VS Code + Playwright — checklist de prontidão bloqueante, padronização de render e tela piloto com baseline de fidelidade medida. Use quando o orquestrador indicar a etapa 4, ou para conectar/validar/calibrar o pipeline Figma-código.
---

# Etapa 4 — MCP (conexão + calibração)

A IA ganha olhos no design real — e aqui se define COMO esses olhos medem.

## Pré-voo
Repo pós-INSTALL (cenário A) ou pós-ONBOARD parcial (B/C) · arquivo Figma
acessível · permissão pra instalar o Playwright MCP · FONTES resolvidas:
preencha `docs/fonts-checklist.md` (de `templates/fonts-checklist.md`) —
licença + instalação + anti-fallback — ANTES da pilota; fallback silencioso
invalida qualquer diff.

## Processo

1. **M1 · Conexão verificada**: bridge/MCP ativo; teste com leitura real de
   um frame E um export de asset. Qualquer falha → BLOQUEIO (nada de seguir
   "no escuro").
2. **M2+M5 · Checklist de prontidão (bloqueante)**: gere
   `docs/figma-checklist.md` a partir de `templates/figma-checklist.md`. Critérios mínimos, todos verificáveis:
   - 100% dos containers com auto-layout (exceções listadas e justificadas)
   - Nomes semânticos do glossário (zero "Frame 427")
   - Cor, tipo, espaçamento e raio via variables — zero valor solto
   - Componentes com variantes p/ TODOS os estados que a spec exige
   - Convenção de handoff escrita: componente vs. variante vs. token vs.
     instância
   Reprovação em qualquer critério = frame não entra na etapa 6. Sem "quase".
3. **Padronização de render** (a metade esquecida do pixel-perfect):
   registre no checklist os parâmetros de verificação do produto — larguras
   de viewport por breakpoint (= larguras dos frames), deviceScaleFactor 2,
   fontes instaladas (família+pesos, com checagem anti-fallback), método de
   diff (pixelmatch/odiff + threshold de anti-aliasing).
4. **M4 · Playwright MCP**: instale e valide com um screenshot real.
5. **M3 · Tela piloto (baseline)**: uma tela simples, ciclo completo da
   fw-ui (extração → geração → diff). Anote: % de diff final, nº de ciclos,
   causas das divergências. Grave a baseline no kfe-state e as causas
   como primeiras entradas do `docs/calibration.md`.
6. **Golden screen**: congele a piloto aprovada como regressão do pipeline —
   crie `tests/golden/<tela>/` (figma.png, render.png, params.md) seguindo
   `templates/golden-readme.md` (copie-o para tests/golden/README.md).

## Definição de pronto
Conexões validadas · checklist bloqueante publicado com parâmetros de render
· piloto aprovada pelo humano · baseline + calibração iniciadas.

## Gate (humano)
Compara piloto vs. Figma e aprova. Cada correção apontada vira regra
(CLAUDE.md ou calibration.md) ANTES da etapa 6 abrir. Regras: Figma é a
verdade absoluta; sem auto-layout, sem geração; nunca compensar arquivo
bagunçado com prompt. Protocolos: `.claude/skills/kill-front-end/protocols.md`.
