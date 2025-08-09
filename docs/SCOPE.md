# Escopo do Projeto (Atualizado) — Plugin GADM para GLPI

## Visão Geral
Este projeto **não altera o core do GLPI**. Em vez disso, fornece um **plugin** chamado `gadm` que acrescenta módulos administrativos voltados à gestão predial do COPPEAD/UFRJ.

## Objetivos
- **Centralizar** a abertura e o acompanhamento de chamados prediais.
- **Controlar Inventário** (consumíveis) com ponto de reposição e baixa automática.
- **Gerenciar Requisições** de materiais com **aprovação do Gerente** (justificativa obrigatória) e **notificações por e-mail**.
- **Patrimônio**: cadastro, localização, responsável, histórico de movimentações/manutenções e anexos.
- **Contratos**: cadastro e **alertas de vencimento** (30/60/90 dias, configurável).
- **Relatórios/Dashboards** por perfil.
- **Backup**: manual (download) e diretrizes para automático via SO.

## Perfis e Direitos
- **Administrador**: acesso total ao plugin e suas configurações.
- **Gerente**: gerencia Inventário, aprova Requisições, gerencia Patrimônio e Contratos.
- **Técnico**: atende chamados prediais, atualiza status; leitura de Inventário.
- **Usuário**: solicita materiais (catálogo) e abre chamados.

## Módulos do Plugin
1. **Inventário (consumíveis)**  
   - Tabela: `glpi_plugin_gadm_inventario_itens`
   - Campos: código, descrição, unidade, estoque atual, estoque mínimo, local de armazenamento, ativo/inativo.
2. **Requisições de Materiais**  
   - Tabelas: `glpi_plugin_gadm_requisicoes`, `glpi_plugin_gadm_requisicao_itens`  
   - Fluxo: Solicitada → Aprovada/Recusada → Em separação → Entregue (baixa de estoque).
   - Regras: justificativa obrigatória; bloqueio se estoque insuficiente; justificativa na recusa.
3. **Patrimônio**  
   - Tabelas: `glpi_plugin_gadm_patrimonios`, `glpi_plugin_gadm_patrimonio_movs`
   - Campos: tombamento, série, aquisição, valor, localização, responsável, status; histórico de movimentações/manutenções.
4. **Contratos + Lembretes**  
   - Tabela: `glpi_plugin_gadm_contratos`
   - Cron: verifica contratos e envia e-mails de alerta a N dias do vencimento (configurável).
5. **Relatórios/Dashboard**  
   - Listas com `rawSearchOptions`, exportações CSV/PDF, cards por perfil (pendências, abaixo do mínimo, vencimentos).
6. **Backup**  
   - Botão para backup manual (dump + anexos do plugin); rotina automática via SO (cron).

## Notificações
- Eventos principais: abertura/atualização de requisição, aprovação/recusa, entrega, alerta de contratos.
- Templates personalizáveis no plugin.

## Integrações
- **LDAP/AD**: autenticação; perfis/direitos definidos no GLPI + direitos específicos do plugin.
- **E-mail SMTP**: para notificações.
