# Protocolos comuns do Framework (v2)

Toda skill fw-* herda estes protocolos. A skill da etapa define O QUE; aqui
está o COMO padrão.

## Pré-voo (antes de executar qualquer etapa)

1. Os artefatos de entrada listados pela skill existem? (ex.: fw-ui exige
   tokens pareados + checklist Figma + skill do projeto)
2. O ambiente responde? (MCP do Figma quando a etapa lê design; Playwright
   quando testa; lint/build quando gera código)
3. O estado está coerente? (etapa anterior `concluída`)
Falhou qualquer item → status `bloqueada(<motivo>)`, reporte no formato de
falha, NÃO improvise contorno.

## Definição de pronto (para concluir qualquer etapa)

- Todos os artefatos da skill existem nos caminhos padrão.
- Checagens automáticas verdes quando houver código: `lint`, `tsc --noEmit`,
  `build` (e testes da etapa, quando existirem).
- Nada pendente marcado como "depois" sem registro em Exceções aprovadas.

## Protocolo de falha / escalada

Ao travar (3 tentativas no mesmo problema, pré-voo reprovado, ou decisão que
não é sua):
```
BLOQUEIO · <etapa> · <passo>
O que tentei: <1–3 linhas>
Causa provável: <hipótese>
Preciso de: <decisão humana | correção no Figma | acesso | informação>
Opções: (a) ... (b) ...
```
Nunca esconda um contorno: gambiarra silenciosa é pior que bloqueio visível.

## Resumo de gate (formato)

```
GATE · <etapa> · <produto>
Feito: <3–6 bullets>
Artefatos: <caminhos>
Para aprovar: <exatamente o que o humano precisa olhar/decidir>
Riscos/exceções: <ou "nenhum">
```

## Idempotência

Toda etapa pode ser re-executada com segurança: antes de criar, verifique se
existe; se existir, atualize por diff (nunca duplique arquivo, seção ou
componente). Re-rodar uma etapa concluída exige confirmação do humano.

## Caminhos padrão

| Artefato | Caminho |
|---|---|
| Estado | docs/framework-state.md |
| Stack e lista negativa | docs/stack.md |
| Contrato de API | docs/api-contract.yaml |
| PRD / regras / glossário | docs/prd.md · docs/regras.md · docs/glossario.md |
| Objetos / specs | docs/objetos/ · docs/specs/ |
| Flows / escopo | docs/flows.md · docs/escopo-v1.md |
| Checklist Figma | docs/figma-checklist.md |
| Calibração de fidelidade | docs/calibration.md |
| Auditoria / onboarding | docs/audit.md · docs/onboard-plan.md |
| ADRs / retro | docs/adr.md · docs/framework-retro.md |
| QA | tests/e2e/ · docs/qa-release.md |
| Handoff | docs/handoff-backend.md |
| Fontes | docs/fonts-checklist.md |
| Métricas | docs/metrics.md |
| Golden screens | tests/golden/ |
| Relatórios de lote | reports/ |
| CI do produto | .github/workflows/framework.yml |
| Calibração global | <kit>/calibration-global.md |
