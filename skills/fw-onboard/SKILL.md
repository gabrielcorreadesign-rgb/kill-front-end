---
name: fw-onboard
description: Onboarding de produto existente no Framework de IA — modo pareamento (cenário B, com design system) ou engenharia reversa (cenário C, sem DS ou incerto). Prepara tokens, paridade, docs retroativas e infraestrutura até o produto ficar pronto para o modo new-screens. Use após fw-audit, quando o orquestrador rotear cenários B ou C.
---

# fw-onboard — Onboarding de produto existente

Entrada obrigatória: `docs/audit.md` aprovado. O modo vem do cenário
confirmado no gate da auditoria.

## Modo B — pareamento (existe DS de verdade)

1. **Tokens**: gere o mapa Figma variable → token do config, 1:1 por nome.
   Divergência de nome → renomear (preferindo o Figma como canônico) e
   registrar no glossário. Zero token sem par.
2. **Componentes**: transforme as 3 listas da auditoria em plano: pareados
   (ok) · só-código (criar par no Figma OU marcar interno sem par visual —
   decisão humana) · só-Figma (backlog de implementação).
3. **Docs retroativas**: o que faltar de stack.md, glossário, regras e specs
   das áreas ativas — escreva documentando O QUE É (modo retroativo: retratar,
   não decidir). PRD só se o humano quiser.
4. **Infraestrutura**: skill do projeto + CLAUDE.md + checklist Figma +
   hooks, via fw-install em modo "sobre repo existente" (não recriar o que
   existe; completar o que falta).
5. **Piloto de calibração**: rode a tela piloto da fw-mcp numa tela nova
   pequena para medir a baseline de fidelidade deste produto.

## Modo C — engenharia reversa (sem DS ou incerto)

1. **Extração de fato**: minere o código: paletas usadas (por frequência),
   escalas de tipo e espaçamento reais, raios, sombras. Cruze com o Figma.
   Saída: proposta de conjunto canônico de tokens (o menor conjunto que
   cobre 90%+ do que existe) + lista do que vira exceção a migrar.
2. **Fonte canônica**: GATE imediato — o humano decide onde o DS mora
   (regra do framework: Figma). Criam-se as variables no Figma a partir do
   conjunto aprovado.
3. **DS retroativo mínimo**: NUNCA big-bang. Construa só o necessário para
   as telas-alvo do primeiro lote: primitivos + componentes que elas usam,
   com par no Figma, migrando os valores soltos dessas rotas para tokens.
   O resto do produto migra lote a lote, guiado por demanda.
4. **Docs + infraestrutura**: como no modo B (passos 3–4).
5. **Piloto de calibração**: idem modo B.

## Definição de pronto
Mapa de tokens 1:1 · plano de paridade com donos · docs mínimas + skill +
CLAUDE.md + checklist no repo · `docs/onboard-plan.md` (o que foi feito, o
que ficou de backlog) · baseline de fidelidade registrada no estado.

## Gate (humano)
Modo B: aprova o mapa de tokens e as decisões de paridade. Modo C: aprova o
conjunto canônico + fonte + escopo do DS mínimo. Depois disso o produto
entra no modo new-screens. Protocolos: `.claude/skills/framework/protocols.md`.
