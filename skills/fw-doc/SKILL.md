---
name: fw-doc
description: Etapa 7 do Kill Front-End — DOC. Pipeline de documentação automática — extrai doc dos componentes pro design system, sincroniza regras de negócio na SRS e registra ADRs. Use quando o orquestrador indicar a etapa 7, ao fim de cada lote da etapa 6, ou quando o usuário pedir para atualizar a documentação de um produto do framework.
---

# Etapa 7 — DOC

Doc automática ou doc mentirosa: toda doc que depende de alguém lembrar vai
mentir em 30 dias. Esta etapa roda ao fim de CADA lote da UI, não uma vez.

## Pré-voo
Lote da fw-ui recém-fechado (esta etapa roda por lote, nunca "no final"); pipeline de extração funcionando — se o passo manual apareceu, conserte o pipeline antes.

## Processo

1. **C1 · Auditoria de doc no código**: varra os componentes do lote. Cada um
   tem doc no padrão (descrição, props, exemplo)? Sem doc → escreva agora,
   lendo o código. Componente sem doc não entra no DS.
2. **C2 · Pipeline → DS**: extraia a doc e atualize o catálogo/página
   /design-system do produto. Sem mão humana: se o processo exigiu passo
   manual, conserte o pipeline antes de seguir.
3. **C3 · Sincronizar regras**: decisões de negócio tomadas durante o lote
   (novas regras, mudanças de estado, exceções) voltam pra `docs/regras.md`
   e pras specs. A SRS continua viva — a IA da próxima sessão gera contra
   regras atuais, não mortas.
4. **C4 · ADRs**: cada desvio de padrão aprovado no lote vira uma entrada em
   `docs/adr.md`: data, o que desviou, por quê, quem aprovou. Três linhas
   bastam.
5. **Paridade**: rode a auditoria Figma ↔ código do lote. Componente órfão
   de um lado → reporte no gate da UI.

## Definição de pronto (artefatos)

- Catálogo/página /design-system atualizada com o lote
- `docs/regras.md` e specs sincronizadas · `docs/adr.md` com os desvios

## Gate (técnico)

Checklist verde: todo componente do lote com doc, pipeline rodou sem passo
manual, zero órfão de paridade (ou órfãos reportados). Sem aprovação humana
dedicada — o resultado aparece no gate da UI.

## Regras

- Doc é parte da definição de pronto, não um extra.
- Desvio sem ADR é bug esperando ser "corrigido" de volta.

Protocolos comuns: `.claude/skills/kill-front-end/protocols.md`.
