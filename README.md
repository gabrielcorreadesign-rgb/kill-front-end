# Framework de IA — Kit de Skills (v2.5)

Sistema de skills que executa o Framework de IA — agnóstico de empresa e
projeto: qualquer produto novo, produto existente ou design system de
cliente. Da definição de stack à entrega, com humano orquestrador nos gates e
geração **pixel-perfect medida** (diff de pixels com limiar, não "parecido").

## O que mudou na v2

- **3 cenários de entrada**: A produto novo · B produto existente com design
  system · C produto existente sem DS (ou incerto) — com `fw-audit`
  (diagnóstico por evidência) e `fw-onboard` (pareamento ou engenharia
  reversa) para B/C.
- **Pixel-perfect como protocolo**: extração exata via MCP (nunca estimar),
  assets exportados do Figma (nunca redesenhados), verificação por diff de
  pixels (aceite: ≤ 1% e geometria zero-divergente), fontes com checagem
  anti-fallback, e `docs/calibration.md` — o livro-razão que converte cada
  divergência recorrente em regra, fazendo o ajuste humano tender a zero.
- **Protocolos comuns** (`skills/framework/protocols.md`): pré-voo, definição
  de pronto, protocolo de falha/escalada, formato de gate, idempotência e
  caminhos padrão — herdados por todas as etapas.
- **Estado v2**: cenário, baseline de fidelidade (da tela piloto) e registro
  de exceções aprovadas.

## Passo a passo

Guia prático de uso (por cenário, com quem-faz-o-quê): **GUIA.md**.

## Instalação

```bash
# no repo do produto (recomendado)
cp -r skills/* <repo>/.claude/skills/
cp commands/*  <repo>/.claude/commands/
# ou global: ~/.claude/skills/ e ~/.claude/commands/
```

## Uso

| Comando | O que faz |
|---|---|
| `/framework-new-product` | Cenário A — etapas 1→9 |
| `/framework-new-ds` | Design system como entrega (cliente novo: DS primeiro, telas depois) |
| `/framework-onboard` | Cenários B/C — fw-audit → fw-onboard → pronto p/ new-screens |
| `/framework-new-screens` | Telas novas em produto onboardado — 5-lite→9 |
| `/framework-next` | Continua do ponto atual (o loop) |
| `/framework-loop` | Loop contínuo — para só em gate humano, bloqueio ou fim |
| `/framework-status` | Estado e próximo gate, sem executar |
| `/framework-dashboard` | Painel visual gamificado do estado (localhost:4242, auto-atualiza) |

Estado em `docs/framework-state.md` — sobrevive entre sessões.

## Conteúdo do kit

`skills/` (12) · `commands/` (6) · `templates/` (esqueletos de todos os
artefatos docs/) · `scripts/` (pixel-diff · framework-dashboard · lote-report) · `calibration-global.md` · `install.sh` · CHANGELOG.md

## Mapa das skills

`framework` (orquestra + protocols.md) · `fw-audit` · `fw-onboard` ·
`fw-stacks` · `fw-srs` · `fw-install` · `fw-mcp` · `fw-ux` · `fw-ui` ·
`fw-doc` · `fw-qa` · `fw-github`

## Gates

STACKS · SRS · AUDIT (cenário) · ONBOARD (tokens/fonte canônica) · MCP
(piloto + baseline) · **UX (o gate forte)** · UI (por lote, com % de diff) ·
QA (preview) · GITHUB (final). INSTALL e DOC: gate técnico.

## Princípios

Humano decide, IA executa · Figma é a verdade absoluta · nunca inventar
valor (sem dado → perguntar, jamais estimar) · nada de código antes do
INSTALL/ONBOARD · repetiu 2x vira infraestrutura · back entregue pronto pra
implementação manual, nunca implementado · todo projeto alimenta o framework.
