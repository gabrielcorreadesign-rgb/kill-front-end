---
name: fw-srs
description: Etapa 2 do Framework de IA — SRS. Gera a documentação global do projeto (PRD, objetos de domínio, regras de negócio, specs por área, glossário) e a skill do projeto. Use quando o orquestrador indicar a etapa 2, ou quando o usuário pedir a documentação-fonte de um produto do framework.
---

# Etapa 2 — SRS

A doc explica o produto para humanos; a skill comanda a geração para a IA.
São dois artefatos, dois papéis. Nunca fundir.

## Pré-voo
`docs/stack.md` aprovado (a SRS escreve sobre a stack decidida); acesso ao humano para as perguntas de PRD — sem ele presente, não conclua D1.

## Processo

1. **D1 · PRD** (`docs/prd.md`): o que é, pra quem, proposta de valor — e a
   seção NÃO-ESCOPO explícita (mínimo 5 itens). Entreviste o humano; não
   invente posicionamento.
2. **D2 · Objetos** (`docs/objetos/<entidade>.md`, um por entidade): prosa
   curta + shape de dados (campos, tipos, relações). Esses arquivos são a
   fonte dos tipos TS e dos mocks — escreva-os pensando nisso.
3. **D3 · Regras** (`docs/regras.md`): acesso e planos, estados possíveis,
   transições, cobrança. Escritas como regra ("usuário free vê X, não Y"),
   nunca como código.
4. **D4 · Specs** (`docs/specs/<area>.md`, uma por área/tela): estados,
   exceções, comportamento. Teste de granularidade: a spec cabe inteira num
   prompt junto com o código da área? Se não cabe, divida.
5. **D6 · Glossário** (`docs/glossario.md`): nome canônico de cada coisa,
   idioma decidido na STACKS aplicado. Um conceito = um nome.
6. **D5 · Skill do projeto** (`.claude/skills/<produto>-frontend/SKILL.md`):
   destile TUDO — stack, lista negativa, convenções, estrutura, 1 exemplo de
   componente correto, referências por caminho para docs/. Enxuta: regras
   operacionais, não prosa. Preencha o contrato OpenAPI com as rotas que os
   objetos e regras implicam.

## Definição de pronto (artefatos)

- `docs/prd.md` · `docs/objetos/*` · `docs/regras.md` · `docs/specs/*`
- `docs/glossario.md` · skill do projeto v1 · `docs/api-contract.yaml` com rotas

## Gate (humano)

O humano revisa PRD + não-escopo + regras de negócio. Objetos e specs são
apresentados em resumo; ele mergulha se quiser.

## Regras

- Doc nasce ANTES do código que governa. Doc depois é ata; antes é contrato.
- Não invente regra de negócio: pergunta aberta > suposição registrada.

Protocolos comuns: `.claude/skills/framework/protocols.md`.
