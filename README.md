# GADM — Plugin de Gerência Administrativa para GLPI 10.x

> **Objetivo**: Estender o GLPI com um plugin focado na **gerência administrativa predial** do COPPEAD/UFRJ: chamados prediais, patrimônio, inventário (consumíveis), **requisições de materiais** com aprovação, e **lembretes de contratos**.

- **Base**: plugin GLPI (sem alterar o core).
- **Perfis**: Administrador, Gerente, Técnico, Usuário.
- **Módulos**: Inventário, Requisições, Patrimônio, Contratos (alertas), Relatórios/Dashboard, Backup.
- **Notificações**: via e-mail + avisos no sistema.
- **Autenticação**: LDAP/AD + contas locais (prestadores).

📄 Documentação completa em [`/docs`](./docs).

---

## Quickstart (resumo)
1. **Instalar GLPI 10.x** em Ubuntu (Apache/Nginx + PHP 8.1+ + MySQL/MariaDB).
2. **Copiar o plugin** `gadm/` para `GLPI_ROOT/plugins/`.
3. No GLPI: **Configuração → Plugins → GADM → Instalar/Ativar**.
4. **Perfis**: ajuste direitos do plugin para Admin/Gerente/Técnico/Usuário.
5. Acesse **Central → Gerência Administrativa → Inventário (consumíveis)** para validar.

> Passo a passo detalhado: veja [`docs/SETUP.md`](./docs/SETUP.md).

---

## Estrutura do repositório
```
.
├── plugins/
│   └── gadm/              # (opcional) plugin dentro do repo (ou submódulo)
├── docs/                  # documentação do projeto
│   ├── SCOPE.md
│   ├── ARCHITECTURE.md
│   ├── SETUP.md
│   ├── ROADMAP.md
│   ├── REQUIREMENTS.md
│   ├── TESTING.md
│   ├── SECURITY.md
│   ├── CONTRIBUTING.md
│   └── CHANGELOG.md
└── LICENSE.md             # a definir pelo mantenedor
```

## Licença
A definir pelo mantenedor do projeto (ex.: GPLv2+ para alinhamento com ecossistema GLPI).

---

*Gerado em 2025-08-09 17:46.*
