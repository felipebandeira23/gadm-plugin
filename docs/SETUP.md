# SETUP — Como iniciar o projeto (passo a passo)

> Guia detalhado para **instalar o GLPI**, preparar o ambiente e subir o **plugin GADM**.

---

## 1) Preparar servidor Ubuntu
Atualize o sistema:
```bash
sudo apt update && sudo apt -y upgrade
sudo reboot
```

Instale dependências (ex.: Apache, PHP e extensões, MariaDB):
```bash
sudo apt -y install apache2 mariadb-server
sudo apt -y install php php-cli php-common php-curl php-gd php-intl php-xml php-mbstring php-zip php-mysql php-ldap
sudo a2enmod rewrite
sudo systemctl restart apache2
```

Configure o banco:
```bash
sudo mysql_secure_installation
# crie DB/usuário para o GLPI (exemplo)
mysql -u root -p -e "CREATE DATABASE glpi_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
mysql -u root -p -e "CREATE USER 'glpi_user'@'localhost' IDENTIFIED BY 'SenhaForteAqui';"
mysql -u root -p -e "GRANT ALL PRIVILEGES ON glpi_db.* TO 'glpi_user'@'localhost'; FLUSH PRIVILEGES;"
```

## 2) Instalar GLPI 10.x
Baixe e extraia o pacote do GLPI para o Apache (ajuste a versão conforme seu download):
```bash
cd /var/www/html
sudo tar -xzf /caminho/para/glpi-10.x.tgz
sudo mv glpi-10.* glpi
sudo chown -R www-data:www-data /var/www/html/glpi
```

Acesse no navegador: `http://SEU_IP/glpi` e siga o **assistente**:
- informe o banco (`glpi_db`, `glpi_user`/senha), 
- crie o usuário admin padrão e finalize.

> Depois de instalar, faça login e ative **Configuração → Segurança → Modo de manutenção** quando for mexer em plugins.

## 3) Preparar o repositório do projeto (GitHub)
No seu PC (desenvolvimento):
```bash
mkdir gadm && cd gadm
git init
git remote add origin https://github.com/SEU_USUARIO/gadm.git
mkdir docs plugins
# copie a documentação deste pacote para ./docs
# e (opcionalmente) mantenha o plugin dentro do repo em ./plugins/gadm
git add .
git commit -m "chore: bootstrap repo docs + structure"
git push -u origin main
```

## 4) Instalar o plugin GADM (skeleton)
Baixe o **skeleton** do plugin e coloque em `GLPI_ROOT/plugins/gadm/`:
```bash
sudo mkdir -p /var/www/html/glpi/plugins/gadm
# copie os arquivos do plugin para essa pasta
sudo chown -R www-data:www-data /var/www/html/glpi/plugins/gadm
```

No GLPI: **Configuração → Plugins → GADM → Instalar/Ativar**.  
Se necessário, limpe cache:
```bash
cd /var/www/html/glpi
sudo -u www-data php bin/console cache:clear
```

## 5) Ajustar perfis e validar primeiro módulo
- Vá em **Administração → Perfis** e conceda direitos do plugin (Admin/Gerente/Técnico/Usuário).
- Acesse **Central → Gerência Administrativa → Inventário (consumíveis)** e **crie um item**.
- Crie 2–3 itens com estoque e mínimo para testes.

## 6) Implementar Requisições (primeira entrega funcional)
- Cadastrar itens → Usuário solicita → Gerente aprova/recusa (com justificativa) → Entrega (baixa estoque).
- Ativar **notificações por e-mail** e testar os 4 eventos (solicitada/aprovada/recusada/entregue).

## 7) Contratos + alertas (cron)
- Cadastrar um contrato com data de vencimento próxima.
- Habilitar cron do plugin (via GLPI ou CLI).
- Validar e-mail de alerta nos prazos configurados.

## 8) Patrimônio
- Cadastrar patrimônio, movimentar localização/responsável, anexar documentos.
- Gerar relatórios por localização/status.

## 9) Backups
- Manual: botão no plugin para gerar dump e baixar.
- Automático (SO): `cron` semanal com dump + cópia de anexos (pasta do plugin).

## 10) Boas práticas
- Nunca alterar o **core** do GLPI.
- Usar **branches** (`dev` para features, `main` estável).
- Fazer commits pequenos e claros.
- Testar em homolog antes de produção.
