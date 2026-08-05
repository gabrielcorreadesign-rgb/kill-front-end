---
name: fw-audit
description: Diagnóstico de produto existente para o Kill Front-End — audita código, Figma, paridade e documentação, e classifica o cenário (B com design system, C sem/incerto) com evidências. Use antes de onboardar qualquer produto existente, quando o usuário não sabe o estado do DS, ou quando o orquestrador rotear cenários B/C.
---

# fw-audit — Diagnóstico de produto existente

Objetivo: substituir "acho que tem um DS" por evidência. Saída única:
`docs/audit.md` (a partir de `templates/audit.md`) com classificação e gaps.

## Pré-voo
Acesso ao repositório; arquivo Figma do produto aberto/acessível via MCP
(se não houver Figma, registre — isso por si só define o cenário C).

## Processo

1. **Código — tokens**: o config de estilo (Tailwind/CSS vars) define
   tokens nomeados? Meça a disciplina: conte valores soltos (hex, px
   arbitrários) em `className`/styles vs. uso de tokens. Reporte a razão
   (ex.: "78% tokens · 22% soltos").
2. **Código — componentes**: existe pasta de componentes reutilizados?
   Amostre 10 telas: quantos elementos vêm de componentes vs. markup ad-hoc?
   Detecte duplicatas por semelhança de nome/função (Card/CardItem/ItemCard).
3. **Figma — fundações**: variables definidas? Componentes com variantes?
   Auto-layout predominante? Rode o espírito do checklist de prontidão numa
   amostra de 5 frames e reporte aprovação por critério.
4. **Paridade**: cruze componentes do código com os do Figma. Três listas:
   pareados · só no código · só no Figma.
5. **Docs e infraestrutura**: existem stack.md, PRD/regras, glossário, skill
   do projeto, CLAUDE.md? O que está desatualizado (bate com o código?).
6. **Classificação**: proponha B (DS real: tokens disciplinados nos DOIS
   lados + maioria pareada) ou C (qualquer outro caso) com as evidências.
   Na dúvida entre B e C, classifique C — onboarding B com base podre
   contamina tudo.

## Definição de pronto
`docs/audit.md` com: métricas por seção, as 3 listas de paridade, gaps
priorizados, classificação proposta + justificativa.

## Gate (humano)
O humano confirma o cenário e escolhe as telas-alvo do primeiro lote (o
onboarding C usa isso para escopo). Siga: protocolos comuns em
`.claude/skills/kill-front-end/protocols.md`.
