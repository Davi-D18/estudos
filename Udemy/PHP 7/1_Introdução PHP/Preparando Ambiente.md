# Apache, XAMPP e PHP

## **Apache**

### **O que é?**

- O Apache HTTP Server é um **servidor web** de código aberto.
- Sua função principal é **servir páginas web** para o navegador do usuário.
- É amplamente utilizado por sua **flexibilidade**, **robustez** e por ser compatível com **diversos sistemas operacionais** (Windows, Linux, macOS).

### **Função Principal:**

- **Recebe solicitações HTTP** e entrega páginas web.
- Executa scripts PHP, se configurado corretamente.
- Hospeda sites e **aplicações dinâmicas**.

### **Como o Apache funciona com PHP:**

1. O Apache serve arquivos **HTML, CSS e JS** (arquivos estáticos).
2. Quando encontra um arquivo **PHP**, o Apache **encaminha** para o interpretador PHP.
3. O **resultado do script PHP** (como HTML gerado dinamicamente) é enviado ao navegador do usuário.

### **Configuração do PHP no Apache:**

- Configurado via módulo **mod_php** ou **CGI**.
- **Arquivos importantes**:
    - `httpd.conf` (configurações principais do Apache)
    - `php.ini` (configurações do PHP)

### **Principais Comandos (Linux):**

- **Iniciar o Apache:**
    
    `sudo service apache2 start`
    
- **Parar o Apache:**
    
    `sudo service apache2 stop`
    
- **Reiniciar o Apache:**
    
    `sudo service apache2 restart`
    
- **Local do arquivo de configuração:**
    
    - `/etc/apache2/httpd.conf` (Linux)
    - `C:/xampp/apache/conf/httpd.conf` (no XAMPP)

---

## **XAMPP**

### **O que é?**

- XAMPP é um pacote de software que inclui **Apache**, **MySQL (ou MariaDB)**, **PHP** e **Perl**.
- Facilita a criação de um **ambiente de desenvolvimento local** para testar e desenvolver aplicações web.
- É multiplataforma (Windows, macOS e Linux) e fácil de instalar.

### **Estrutura do XAMPP:**

- Ao instalar o XAMPP, ele cria a seguinte estrutura de diretórios:
    - **htdocs/**: Onde você coloca seus arquivos PHP (geralmente `C:/xampp/htdocs`).
    - **apache/**: Contém o servidor Apache e seus arquivos de configuração.
    - **mysql/**: Diretório com arquivos do banco de dados MySQL/MariaDB.
    - **php/**: Contém a instalação do PHP e seu arquivo `php.ini`.
    - **phpMyAdmin/**: Ferramenta para gerenciar o banco de dados via navegador.

### **Componentes do XAMPP:**

- **Apache**: O servidor web que servirá as páginas e processará o PHP.
- **MySQL/MariaDB**: Banco de dados para armazenar dados de sua aplicação.
- **PHP**: Linguagem de programação para o desenvolvimento de páginas dinâmicas.
- **phpMyAdmin**: Interface gráfica para gerenciar seus bancos de dados.

### **Como Usar o XAMPP com PHP:**

1. **Instale o XAMPP** do site oficial Apache Friends.
    
2. **Inicie o Apache e o MySQL** pelo "XAMPP Control Panel".
    
3. **Coloque os arquivos PHP** dentro da pasta `htdocs` (ex: `C:/xampp/htdocs/meu_arquivo.php`).
    
4. **Acesse no navegador**:
    
    `http://localhost/meu_arquivo.php`
    
5. Para gerenciar bancos de dados, use o **phpMyAdmin**:
    
    `http://localhost/phpmyadmin`
    

### **Principais Funções do XAMPP:**

- Facilitar o **desenvolvimento local** de aplicações PHP.
- Simular um **ambiente de produção** no seu computador.

### **Comandos e Ações (Windows):**

- **Iniciar Apache e MySQL**: Use o "XAMPP Control Panel" ou:
    - **Iniciar manualmente**: `xampp_start.exe`.
    - **Parar manualmente**: `xampp_stop.exe`.
- **Acessar o phpMyAdmin**:
    
    `http://localhost/phpmyadmin`
    

---

## **PHP no Apache/XAMPP**

### **O que é PHP?**

- **PHP** (Hypertext Preprocessor) é uma linguagem de programação voltada para o desenvolvimento web, usada para criar páginas dinâmicas.

### **Como o PHP funciona no Apache?**

1. Quando um **arquivo PHP** é requisitado, o Apache delega a execução ao **interpretador PHP**.
2. O resultado da execução (geralmente HTML) é enviado ao navegador.

### **Estrutura Básica de um Arquivo PHP:**

```php
<?php   
	echo "Olá, mundo!"; 
?>
```

- O código PHP é delimitado pelas tags `<?php ?>` e seu resultado é **renderizado no navegador** como HTML.

### **Configurando PHP no XAMPP:**

- O PHP no XAMPP já vem configurado. Para ajustar algumas configurações:
    - Arquivo de configuração: **`php.ini`**.
    - Localização do arquivo: `C:/xampp/php/php.ini`.
    - Configurações importantes no `php.ini`:
        - **memory_limit**: Limita a quantidade de memória que um script PHP pode utilizar.
        - **upload_max_filesize**: Define o tamanho máximo de arquivos enviados por upload.
        - **max_execution_time**: Tempo máximo de execução de um script.

### **Funções PHP Importantes:**

- **echo**: Imprime uma string ou variável no navegador.
    
    `echo "Olá, Mundo!";`
    
- **include() / require()**: Inclui arquivos PHP em outros arquivos.
    
    php
    
    Copiar código
    
    `include 'cabeçalho.php';`
    
- **$_GET / $_POST**: Recebe dados de formulários ou URLs.
    
    php
    
    Copiar código
    
    `$nome = $_GET['nome'];`
    
- **mysqli_connect()**: Conecta ao banco de dados MySQL.
    
    php
    
    Copiar código
    
    `$conexao = mysqli_connect("localhost", "usuario", "senha", "banco");`
    

---

## **Boas Práticas e Dicas**

- **Organize seus arquivos PHP** dentro de subpastas dentro de `htdocs` para facilitar a manutenção.
- **Desabilite a exibição de erros** em ambientes de produção, modificando `display_errors` no arquivo `php.ini`.
- Faça **testes locais** no XAMPP antes de migrar sua aplicação para produção.
- Use **phpMyAdmin** para gerenciar bancos de dados com facilidade.