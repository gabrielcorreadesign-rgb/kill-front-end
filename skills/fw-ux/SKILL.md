---
name: fw-ux
description: Etapa 5 do Framework de IA — UX. Design thinking com IA na síntese (pesquisa, user flows, moodboard, corte do MVP). Tem modo completo (produto novo) e modo lite (telas novas). Use quando o orquestrador indicar a etapa 5, ou quando o usuário pedir síntese de pesquisa, fluxos ou definição de escopo de telas.
---

# Etapa 5 — UX

A IA acelera a síntese; a escuta continua humana.

## Pré-voo
Modo completo: PRD existente (o corte v1 conversa com o não-escopo). Modo lite: produto onboardado (stack + skill + checklist no repo) e telas-alvo definidas pelo humano.

## Processo (modo completo — new-product)

1. **U1 · Descoberta**: peça o material bruto (entrevistas, notas, benchmark,
   dados). Se NÃO existir: gere roteiro de entrevista + lista de benchmarks
   sugeridos e PARE — pesquisa não se inventa. Retome quando houver material.
2. **U2 · Síntese**: transcreva/organize, clusterize dores e desejos, extraia
   insights. Apresente como hipóteses ("o material sugere X") — o humano
   valida o que é real e o que é ruído.
3. **U3 · User flows**: desenhe os fluxos principais em Mermaid dentro de
   `docs/flows.md` (um diagrama por jornada). Nenhuma tela antes disso.
4. **U4 · Direção visual**: monte `docs/direcao-visual.md` — referências,
   tom, personalidade, o vocabulário que o DS vai seguir. Proponha; o gosto
   final é do humano.
5. **U5 · Corte da v1**: liste features candidatas e proponha o corte, ligado
   ao não-escopo do PRD. `docs/escopo-v1.md`: o que entra, o que fica pra
   depois, com uma linha de motivo cada.

## Modo lite (new-screens)

Pule U1/U4. Execute: U3 pro fluxo das telas novas (adicione ao flows.md),
U5 mini-corte (o que exatamente entra neste lote) e confira as specs das
áreas novas na SRS — se não existem, crie-as agora (regra D4).

## Definição de pronto (artefatos)

- `docs/flows.md` · `docs/escopo-v1.md` (ou adendo do lote)
- Modo completo: síntese de pesquisa + `docs/direcao-visual.md`

## Gate (humano — FORTE)

Fluxos + corte são decisão de produto. Apresente com opções onde houver
dúvida e espere aprovação explícita item a item. Este é o gate mais
importante do framework: tudo depois dele é execução.

## Regras

- IA sintetiza, humano escuta: nunca invente dado de usuário ou persona.
- Tela nenhuma nasce antes do fluxo aprovado.

Protocolos comuns: `.claude/skills/framework/protocols.md`.
