# TESTING — Testes e Homologação

## Ambientes
- **Desenvolvimento**: sua máquina/VM.
- **Homologação**: VM espelho da produção.
- **Produção**: intranet COPPEAD.

## Planos de teste
- Casos para Inventário (criar, editar, filtros, mínimo).
- Requisições: fluxos completo (aprovada/recusada), notificações e baixa de estoque.
- Contratos: cron e alertas nos prazos.
- Patrimônio: CRUD, anexos, histórico.
- Permissões por perfil.
- Desempenho em listas e exportações.

## Dados de seed (sugestão)
- 10 itens de estoque (com diferentes mínimos).
- 5 patrimônios (locais/responsáveis).
- 2 contratos (um com vencimento em 7 dias).
- 4 usuários (um por perfil).
