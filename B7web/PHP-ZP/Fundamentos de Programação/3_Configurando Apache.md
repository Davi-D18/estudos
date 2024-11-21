### 1. Introdução

O XAMPP é um pacote de software que inclui Apache, MySQL (ou MariaDB), PHP e Perl, facilitando o desenvolvimento local de aplicações web. A seguir, vamos abordar as configurações principais dos arquivos mais relevantes no XAMPP para Linux, com ênfase no Apache e no MySQL.

### 2. Localização dos Arquivos de Configuração

- **Diretório Raiz do XAMPP**: `/opt/lampp/`
    
- **Configuração do Apache**: `/opt/lampp/etc/httpd.conf`
    
- **Configurações Adicionais do Apache**: `/opt/lampp/etc/extra/`
    
- **Configuração do MySQL**: `/opt/lampp/etc/my.cnf`
    
- **Configuração do PHP**: `/opt/lampp/etc/php.ini`
    

### 3. Configurações do Apache

#### 3.1. Arquivo `httpd.conf`

Este é o principal arquivo de configuração do servidor Apache. Algumas das configurações importantes incluem:

- **DocumentRoot**: Define o diretório onde os arquivos do site ficam armazenados.
    
    ```
    DocumentRoot "/opt/lampp/htdocs"
    <Directory "/opt/lampp/htdocs">
        Options Indexes FollowSymLinks ExecCGI
        AllowOverride All
        Require all granted
    </Directory>
    ```
    
- **Porta de Escuta**:
    
    ```
    Listen 80
    ```
    
    Pode ser alterada se você quiser rodar o Apache em outra porta (ex: `Listen 8080`).
    
- **Módulos de Carregamento**: Certifique-se de que os módulos necessários estão habilitados. Exemplo:
    
    ```
    LoadModule rewrite_module modules/mod_rewrite.so
    LoadModule ssl_module modules/mod_ssl.so
    ```
    
    O `mod_rewrite` é essencial para URLs amigáveis, enquanto o `mod_ssl` é usado para conexões seguras (HTTPS).
    
- **Arquivo de Logs**: Configure os logs de acesso e erros:
    
    ```
    ErrorLog "/opt/lampp/logs/error_log"
    CustomLog "/opt/lampp/logs/access_log" combined
    ```
    

#### 3.2. Arquivo `httpd-vhosts.conf`

Localizado em `/opt/lampp/etc/extra/httpd-vhosts.conf`, é usado para configurar hosts virtuais.

```
<VirtualHost *:80>
    ServerAdmin webmaster@exemplo.com
    DocumentRoot "/opt/lampp/htdocs/meuprojeto"
    ServerName meuprojeto.local
    <Directory "/opt/lampp/htdocs/meuprojeto">
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

**Nota**: Adicione a entrada correspondente no arquivo `/etc/hosts` para mapear o domínio `meuprojeto.local` para `127.0.0.1`:

```
127.0.0.1    meuprojeto.local
```

#### 3.3. Configurações de Segurança

- **Desabilitar Listagem de Diretórios**: Certifique-se de que a opção `Indexes` esteja desativada para evitar que o conteúdo dos diretórios seja listado.
    
    ```
    <Directory "/opt/lampp/htdocs">
        Options -Indexes
    </Directory>
    ```
    
- **SSL (HTTPS)**: Ative o SSL adicionando o módulo `mod_ssl` e configurando o arquivo `/opt/lampp/etc/extra/httpd-ssl.conf`.
    

### 4. Configurações do MySQL (`my.cnf`)

- **Porta de Escuta**:
    
    ```
    port = 3306
    ```
    
- **Diretório de Dados**:
    
    ```
    datadir = /opt/lampp/var/mysql
    ```
    
- **Configurações de Performance**:
    
    ```
    max_connections = 200
    query_cache_size = 64M
    ```
    
- **Segurança**:
    
    ```
    skip-networking
    bind-address = 127.0.0.1
    ```
    
    Essas opções ajudam a garantir que o MySQL esteja acessível apenas localmente, aumentando a segurança.
    

### 5. Configurações do PHP (`php.ini`)

- **Erro de Exibição**:
    
    ```
    display_errors = On
    ```
    
    Durante o desenvolvimento, é útil deixar os erros visíveis. Para produção, altere para `Off`.
    
- **Limite de Memória**:
    
    ```
    memory_limit = 256M
    ```
    
- **Tempo de Execução Máximo**:
    
    ```
    max_execution_time = 60
    ```
    


Para criar um servidor local para cada projeto, basta criar uma pasta com o nome do projeto na pasta `htdocs` em seguida, adicionar virtualhosts no arquivo `httpd-vhosts.conf` a configuração dessa parte é preenchida com as informações referentes a pasta do projeto

### 1. Instalando o Apache no Linux

Para instalar o Apache em distribuições baseadas em Debian (como Ubuntu):

```
sudo apt update
sudo apt install apache2
```

Para distribuições baseadas em Red Hat (como CentOS):

```
sudo dnf install httpd
```

### 2. Iniciando e Habilitando o Apache

Inicie e habilite o Apache para que ele inicie automaticamente:

```
sudo systemctl start apache2  # Para Debian/Ubuntu
sudo systemctl enable apache2

sudo systemctl start httpd    # Para CentOS/Red Hat
sudo systemctl enable httpd
```

### 3. Verificando o Status do Servidor

Verifique se o servidor está rodando:

```
sudo systemctl status apache2  # Para Debian/Ubuntu
sudo systemctl status httpd    # Para CentOS/Red Hat
```

### 4. Estrutura de Diretórios do Apache

- **Diretório Raiz dos Sites**:
    
    - Debian/Ubuntu: `/var/www/html`
        
    - CentOS/Red Hat: `/var/www/html`
        
- **Arquivo de Configuração Principal**:
    
    - Debian/Ubuntu: `/etc/apache2/apache2.conf`
        
    - CentOS/Red Hat: `/etc/httpd/conf/httpd.conf`
        
- **Configurações de Hosts Virtuais**:
    
    - Debian/Ubuntu: `/etc/apache2/sites-available/`
        
    - CentOS/Red Hat: `/etc/httpd/conf.d/`
        

### 5. Criando um Novo Projeto

1. **Criar um Novo Diretório para o Projeto**:
    
    ```
    sudo mkdir /var/www/html/meuprojeto
    sudo chown -R $USER:$USER /var/www/html/meuprojeto
    ```
    
2. **Criar um Arquivo de Configuração do Virtual Host**: No Debian/Ubuntu:
    
    ```
    sudo nano /etc/apache2/sites-available/meuprojeto.conf
    ```
    
    No CentOS/Red Hat:
    
    ```
    sudo nano /etc/httpd/conf.d/meuprojeto.conf
    ```
    
    Conteúdo do arquivo:
    
    ```
    <VirtualHost *:80>
        ServerAdmin webmaster@meuprojeto.com
        DocumentRoot "/var/www/html/meuprojeto"
        ServerName meuprojeto.local
        <Directory "/var/www/html/meuprojeto">
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/meuprojeto-error.log
        CustomLog ${APACHE_LOG_DIR}/meuprojeto-access.log combined
    </VirtualHost>
    ```
    
3. **Ativar o Novo Virtual Host** (apenas em Debian/Ubuntu):
    
    ```
    sudo a2ensite meuprojeto.conf
    ```
    
4. **Atualizar o arquivo** `**/etc/hosts**`:
    
    ```
    sudo nano /etc/hosts
    ```
    
    Adicione:
    
    ```
    127.0.0.1 meuprojeto.local
    ```
    
5. **Reiniciar o Apache para Aplicar as Mudanças**:
    
    ```
    sudo systemctl restart apache2  # Para Debian/Ubuntu
    sudo systemctl restart httpd    # Para CentOS/Red Hat
    ```
    

### 6. Testando o Novo Projeto

Abra o navegador e acesse `http://meuprojeto.local` para verificar se o novo projeto está funcionando.

### 7. Dicas de Configuração Adicional

- **Habilitar** `**mod_rewrite**` (para URLs amigáveis):
    
    ```
    sudo a2enmod rewrite  # Para Debian/Ubuntu
    ```
    
    Reinicie o Apache após habilitar.
    
- **Verificar Logs** para diagnosticar problemas:
    
    ```
    tail -f /var/log/apache2/error.log  # Para Debian/Ubuntu
    tail -f /var/log/httpd/error_log    # Para CentOS/Red Hat
    ```
    