---
name: fw-ui
description: Etapa 6 do Framework de IA (v2) — UI pixel-perfect. Motor de geração Figma→código com protocolo de extração exata, verificação por diff de pixels com limiar numérico e registro de calibração. Use quando o orquestrador indicar a etapa 6, ou quando o usuário pedir para gerar componentes ou telas a partir do Figma.
---

# Etapa 6 — UI e IA (pixel-perfect)

Meta: 1:1 com o Figma, medido — não "parecido". O ajuste humano tende a zero
porque (a) só entra frame aprovado no checklist, (b) a extração é exata,
(c) a verificação é objetiva, (d) cada erro vira regra de calibração.

## Pré-voo
Tokens pareados 1:1 · `docs/figma-checklist.md` existente · skill do projeto
e CLAUDE.md no repo · MCP do Figma respondendo · `docs/calibration.md`
existente (crie a partir de `templates/calibration.md` no primeiro uso) ·
GOLDEN SCREEN verde no início do lote e após qualquer mudança de tokens/
dependência de UI (tests/golden/ — FAIL = bloqueio de pipeline, não do lote) · fontes do Figma instaladas no app
(família E pesos exatos — fallback de fonte = reprovação automática).

## Protocolo de extração (por frame — NUNCA estimar)

1. Rode o checklist de prontidão. Reprovou → BLOQUEIO, frame volta pro Figma.
2. Extraia via MCP os valores computados: dimensões, constraints, padding,
   gap, radius, strokes, sombras (x/y/blur/spread/cor/alpha), tipografia
   (família, peso, tamanho, line-height, letter-spacing), opacidades.
3. Cores e medidas SEMPRE resolvidas para o token (variable → token → classe).
   Valor sem variable no Figma = furo do checklist → volta pro Figma.
4. Assets (ícones, imagens, ilustrações): EXPORTE do Figma (SVG/PNG via MCP).
   Proibido redesenhar ou substituir por ícone "equivalente" de biblioteca.
5. Estados (hover/focus/active/disabled/loading): vêm das VARIANTES do frame.
   Estado sem variante desenhada não existe → não invente; registre a
   ausência e siga (ou peça a variante, se o estado for exigido pela spec).

## Protocolo de verificação (por item)

1. Renderize no viewport EXATO do frame (mesma largura; deviceScaleFactor 2;
   mesma fonte carregada — confirme que não houve fallback).
2. Screenshot via Playwright → diff contra o export do frame com
   `node scripts/pixel-diff.js <figma.png> <render.png>` (instale no produto:
   `npm i -D pixelmatch pngjs`). Geometria divergente = FAIL imediato.
3. Aceite: diff ≤ 1,0% dos pixels E zero divergência de geometria (posição/
   tamanho de qualquer elemento). O limiar do produto pode ser apertado em
   `docs/calibration.md`, nunca afrouxado sem exceção aprovada.
4. Reprovou → liste as maiores regiões divergentes com causa provável →
   corrija → repita. Máx. 3 ciclos; persistiu → classifique e escale:
   bug de código (corrigir) · furo do Figma (volta pro design) · limitação
   de render (fonte/subpixel — exceção aprovada, registrada com print).
5. Aprovou → registre o % no log do lote. Todo item entra no gate COM o
   número, não com adjetivo.

## Calibração (o que faz o ajuste desaparecer)

`docs/calibration.md` é o livro-razão: toda divergência recorrente vira
regra de geração (ex.: "line-height px do Figma → leading-[Npx], nunca
leading-relaxed"). Releia no início de cada lote; aplique ANTES de gerar.
Duas ocorrências do mesmo desvio sem regra registrada = falha de processo.

## Ordem e lotes
Fundações → componentes (primitivos → compostos) → telas (só instâncias;
elemento sem componente = criar o par primeiro). Lotes de 1 tela ou 3–5
componentes; ao fim de cada lote: fw-doc + checagens (lint · tsc · build) +
gate.

## Definição de pronto
Itens do lote com diff ≤ limiar e geometria zero-divergente · estados das
variantes implementados · assets exportados (não recriados) · a11y básica
(foco visível, contraste AA nos textos, alt/aria nos assets) · doc do
componente escrita · checagens verdes.

## Gate (humano, por lote)
Apresente por item: screenshot lado a lado + % de diff + exceções. Registre
a linha do lote em `docs/metrics.md` (tempo, itens, diff médio, ciclos,
correções humanas — template em `templates/metrics.md`). Fidelidade
o robô já mediu — o humano avalia o que máquina não vê: sensação, micro-
interação, adequação. Correção apontada 2x → calibration.md antes do próximo
lote. Protocolos: `.claude/skills/framework/protocols.md`.
