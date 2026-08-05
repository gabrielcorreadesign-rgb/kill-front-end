Abra o painel visual do Framework de IA.

Na raiz do produto, execute em segundo plano:
`node <caminho-do-kit>/scripts/framework-dashboard.mjs` e informe ao usuário
a URL (http://localhost:4242). O painel lê docs/framework-state.md e
docs/metrics.md e se atualiza sozinho a cada 3s — nenhuma manutenção manual.
Se o estado não existir ainda, oriente a rodar um comando /framework-* antes.
