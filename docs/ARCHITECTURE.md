# Arquitetura — Plugin GADM

## Stack e Compatibilidade
- **GLPI** 10.x (PHP 8.1+, MySQL/MariaDB).
- Plugin `gadm` em **PHP**, seguindo os padrões do GLPI (pastas `inc/`, `front/`, `locales/`, `install/`).
- Sem alteração do core ⇒ fácil atualização do GLPI.

## Estrutura do plugin
```
plugins/gadm/
  setup.php            # versão, pré-requisitos, metadados
  hook.php             # registro de menus, cron, instalação
  install/             # scripts de migração/upgrade (opcional)
  inc/
    menu.class.php
    profile.class.php
    inventarioitem.class.php
    requisicao.class.php
    requisicaoitem.class.php
    patrimonio.class.php
    patrimoniomov.class.php
    contrato.class.php
    config.class.php
  front/
    inventarioitem.php
    inventarioitem.form.php
    requisicao.php
    requisicao.form.php
    contrato.php
    contrato.form.php
    patrimonio.php
    patrimonio.form.php
    report_*.php
  locales/
    pt_BR.po
  pics/
    icon.png
```

## Padrões de código
- Classes estendem `CommonDBTM` (CRUD, permissões, busca).
- Menus com `CommonGLPI` e hooks em `hook.php`.
- `rawSearchOptions()` nas classes para construir telas de pesquisa.
- Cron via `$PLUGIN_HOOKS['cron']`.
- Traduções via `.po` em `locales/`.

## Segurança e Dados
- Respeitar permissões por perfil (direitos `gadm_*`).
- Logs de alterações (GLPI já registra grande parte).
- Campos críticos validados no back-end (ex.: estoque não negativo).
