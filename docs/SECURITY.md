# SECURITY — Diretrizes

- Acesso apenas pela intranet (sem exposição externa).
- LDAP/AD para autenticação primária; locais para prestadores.
- Perfis/direitos do plugin bem delimitados (princípio do menor privilégio).
- Validações de entrada (ex.: impedir estoque negativo).
- Logs de ações relevantes (core GLPI + logs do plugin quando necessário).
- Backups testados periodicamente (restauração verificada em homolog).
