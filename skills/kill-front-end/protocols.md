# Protocolos comuns do Framework (v2)

Toda skill fw-* herda estes protocolos. A skill da etapa define O QUE; aqui
está o COMO padrão.

## Camadas de verdade (v3.1)

O KFE tem DUAS camadas de verdade, e elas são verificadas de formas
diferentes. Confundir as duas é o erro mais caro do pipeline.

| | Camada 1 — Repouso | Camada 2 — Interação |
|---|---|---|
| O que é | Layout, geometria, tokens, tipografia, espaçamento, o estado default de tela e componente | hover · active · focus · disabled · loading · selected · empty · error · skeleton · motion |
| Fonte | **Figma, verdade absoluta** | Declaração + banco de regras + analogia no registro |
| Onde mora | Arquivo do Figma | `docs/interactions.md` · `<kit>/interactions-global.md` · `docs/components-registry.json` |
| Como se mede | `scripts/pixel-diff.js` contra o export do frame — ≤1,0% e geometria zero-divergente | Golden por estado (`tests/golden/states/`) + `scripts/kfe-interactions.mjs audit` |
| Divergência = | Bug do código | Bug de consistência (regra divergente dentro da família) |

**Cadeia de precedência da camada 2** (obrigatória, por estado, por componente):

1. Variante desenhada no Figma → `figma` (volta a ser camada 1, pixel-diff)
2. Declaração em `docs/interactions.md` → `declarado`
3. Regra do banco (local do produto > global do kit) → `banco`
4. Analogia no registro, **com precedente citado** → `inferido` (provisório, vai ao gate)
5. Nada acima resolve → **BLOQUEIO**, pergunte ao humano → `humano`

Nível 4 sem precedente citável não é inferência: é chute. Chute é bloqueio.
Rode `node <kit>/scripts/kfe-interactions.mjs precedent <Componente> <familia> <estado>`
— se a saída for `PRECEDENTE: NENHUM`, escale pelo protocolo de falha.

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
| Estado | docs/kfe-state.md |
| Stack e lista negativa | docs/stack.md |
| Contrato de API | docs/api-contract.yaml |
| PRD / regras / glossário | docs/prd.md · docs/regras.md · docs/glossario.md |
| Objetos / specs | docs/objetos/ · docs/specs/ |
| Flows / escopo | docs/flows.md · docs/escopo-v1.md |
| Checklist Figma | docs/figma-checklist.md |
| Calibração de fidelidade | docs/calibration.md |
| Auditoria / onboarding | docs/audit.md · docs/onboard-plan.md |
| ADRs / retro | docs/adr.md · docs/kfe-retro.md |
| QA | tests/e2e/ · docs/qa-release.md |
| Handoff | docs/handoff-backend.md |
| Fontes | docs/fonts-checklist.md |
| Métricas | docs/metrics.md |
| Golden screens | tests/golden/ |
| Relatórios de lote | reports/ |
| CI do produto | .github/workflows/kfe.yml |
| Calibração global | <kit>/calibration-global.md |
| Declaração de interações | docs/interactions.md |
| Registro de componentes | docs/components-registry.json |
| Banco global de interações | <kit>/interactions-global.md |
| Golden por estado | tests/golden/states/ |
