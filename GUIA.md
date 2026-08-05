# Guia passo a passo — Framework de IA (v2.3)

O README é a referência; este guia é a receita. Siga na ordem. Legenda:
🧑 = você faz/decide · 🤖 = a IA executa · 🚪 = gate (o loop para e espera você).

---

## 0 · Preparação (uma vez por máquina/produto)

1. 🧑 Extraia o kit e instale: `./install.sh <pasta-do-produto>` (ou `--global`).
2. 🧑 Abra o produto no VS Code com Claude Code; confirme os MCPs: Figma
   (bridge/desktop) e Playwright respondendo.
3. 🧑 No produto: `npm i -D pixelmatch pngjs` (verificação de fidelidade).
4. 🧑 Tenha o arquivo Figma do projeto aberto no Desktop.

Pronto. Daqui em diante, tudo começa com um comando.

---

## Cenário A · Produto novo — `/framework-new-product`

| # | Etapa | O que acontece | Você |
|---|-------|----------------|------|
| 1 | STACKS | 🤖 propõe a base (ou desvios com motivo), lista negativa, fronteira do back | 🚪 aprova stack + desvios. Cliente externo? Diga QUEM implementa o back |
| 2 | SRS | 🤖 te entrevista pro PRD, modela objetos, regras, specs, glossário, skill do projeto | 🚪 revisa PRD + não-escopo + regras |
| 3 | INSTALL | 🤖 monta repo, CLAUDE.md, templates, hooks, lint/CI | 🚪 técnico: lint+build verdes (aprovação rápida) |
| 4 | MCP | 🤖 conecta tudo, gera checklist do Figma, roda a TELA PILOTO com diff medido | 🧑 antes: preencha docs/fonts-checklist.md e desenhe 1 tela simples no Figma · 🚪 aprova a piloto; correções viram regra |
| 5 | UX | 🤖 sintetiza sua pesquisa, desenha flows, propõe corte v1 | 🧑 forneça o material bruto (a IA NÃO inventa pesquisa) · 🚪 FORTE: aprova flows + escopo item a item |
| 6 | UI | 🤖 gera por lote: tokens → componentes → telas, cada item com % de diff | 🧑 desenhe no Figma passando no checklist · 🚪 por lote: screenshots + números |
| 7 | DOC | 🤖 roda o pipeline de doc a cada lote | — (técnico) |
| 8 | QA | 🤖 deriva roteiros das specs, testa, corrige em loop, publica preview | 🚪 teste na URL (celular incluso) e assine o checklist |
| 9 | GITHUB | 🤖 monta o pacote de entrega + handoff do back + retro | 🚪 final: confere pacote, agenda handoff, responde a retro |

Dica de ritmo: rode `/framework-loop` — ele avança sozinho e só para nos 🚪.
`/framework-status` a qualquer momento mostra onde você está.

---

## Cenário B/C · Produto existente — `/framework-onboard`

1. 🤖 `fw-audit` mede: tokens vs. valores soltos, componentização, Figma,
   paridade, docs → `docs/audit.md` com classificação proposta (B ou C).
2. 🚪 Você confirma o cenário e escolhe as telas-alvo do primeiro lote.
3. 🤖 `fw-onboard`:
   - **B (tem DS real)**: mapa de tokens 1:1, plano de paridade, docs
     retroativas, infraestrutura, piloto de calibração.
   - **C (sem DS/incerto)**: minera os tokens de fato do código, propõe o
     conjunto canônico → 🚪 você aprova conjunto + fonte canônica (Figma) →
     DS retroativo MÍNIMO só das telas-alvo (nunca big-bang).
4. 🚪 Gate do onboarding (mapa de tokens / decisões de paridade).
5. A partir daqui o produto está onboardado → use o dia a dia abaixo.

---

## Dia a dia · Telas novas — `/framework-new-screens`

O modo que você mais vai usar:

1. 🧑 Desenhe as telas no Figma passando no checklist do produto.
2. 🧑 `/framework-new-screens` → 🤖 valida pré-requisitos e roda UX-lite
   (flow do lote + specs das áreas novas se faltarem).
3. 🚪 Aprova o mini-escopo do lote.
4. 🤖 `/framework-loop`: UI (com golden screen no início) → DOC → QA →
   entrega parcial. Você aparece nos gates de lote e no preview.

---

## Cliente novo · DS primeiro, telas depois — `/framework-new-ds`

Para o caso "empresa quer o design system, telas vêm depois":

1. Etapas 1–4 normais (a SRS vira o **brief do DS**: marca, princípios,
   não-escopo; o glossário nasce do vocabulário do cliente).
2. UX = direção visual + **inventário de componentes** necessários → 🚪.
3. UI gera SÓ fundações + componentes + **showcase** (página com todo
   componente em todas as variantes — é o produto deste modo) → 🚪 por lote.
4. GITHUB entrega o DS instalável: tokens + componentes + showcase + doc de
   uso e extensão + checklist Figma do cliente.
5. Quando vierem as telas: o produto já é cenário B por construção —
   `/framework-new-screens` direto.

---

## Painel visual (gamificado e automático)

`/framework-dashboard` (ou `node <kit>/scripts/framework-dashboard.mjs` na
raiz do produto) → http://localhost:4242. Mostra a jornada das etapas com
status ao vivo, a missão atual (o que o loop espera de você), conquistas
(piloto, fidelidade ≤1%, lotes, golden, retro, ciclo completo), lotes com
tempo/diff e os últimos eventos do log. Zero manutenção: ele só LÊ o
framework-state.md e o metrics.md que as skills já mantêm — deixe aberto num
monitor enquanto o /framework-loop roda.

## Quando algo trava

- A IA reporta `BLOQUEIO` no formato padrão → leia "Preciso de:" e responda.
- Golden screen FAIL → problema do PIPELINE (tokens/fontes/deps), não da
  tela. Trate antes de qualquer lote.
- Diff não converge em 3 ciclos → decida: bug de código, furo do Figma
  (volta pro design) ou exceção registrada com print.
- Corrigiu a mesma coisa 2x → exija a regra (calibration/CLAUDE.md) antes
  de continuar. É assim que o ajuste desaparece.

## Os 5 comandos, decorados

`/framework-new-product` · `/framework-onboard` · `/framework-new-screens`
· `/framework-new-ds` · `/framework-loop` (+ `/framework-next` passo a
passo e `/framework-status` pra se localizar).
