# REQUIREMENTS — Requisitos

## Funcionais
- Cadastro e manutenção de **Inventário** (consumíveis) com estoque mínimo.
- **Requisições** com justificativa obrigatória, aprovação do Gerente, baixa de estoque e notificações por e-mail.
- **Patrimônio** com histórico de movimentações e anexos.
- **Contratos** com lembretes antes do vencimento (configuráveis).
- Relatórios e dashboard por perfil.
- Backup manual via UI e diretrizes de backup automático no SO.

## Não Funcionais
- Sem alterações no core do GLPI (facilitar upgrades).
- Interface responsiva, em PT-BR, seguindo padrões do GLPI.
- Compatível com GLPI 10.x, PHP 8.1+, MySQL/MariaDB.
- Autenticação com LDAP/AD.
- Logs e trilhas de auditoria aproveitando o core do GLPI.
