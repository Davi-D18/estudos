### **1.Criando um Projeto PHP**

- Navegue até o diretório de instalação do XAMPP. Por padrão, o caminho é:
    
    - **Windows**: `C:\xampp\htdocs`
        
    - **macOS/Linux**: `/opt/lampp/htdocs`
        
- Crie uma pasta dentro de `htdocs` para seu projeto. Por exemplo, `meu_projeto`.
    
- Abra seu editor de código favorito (por exemplo, VS Code) e crie um arquivo PHP chamado `index.php` dentro da pasta `meu_projeto`.
    

```
<?php
  echo "Olá, mundo! Meu primeiro script PHP!";
?>
```

### 2. **Executando o Arquivo PHP no Navegador**

- Abra o navegador e digite a URL:
    
    ```
    http://localhost/meu_projeto/index.php
    ```
    
- Se o servidor Apache estiver rodando corretamente, você deverá ver a mensagem **"Olá, mundo! Meu primeiro script PHP!"** exibida na página.
    

## Dicas Adicionais

- Se você encontrar erros, verifique se o Apache está em execução no painel de controle do XAMPP.
    
- Certifique-se de que a extensão PHP esteja habilitada no arquivo `php.ini` (por padrão, o XAMPP já vem configurado corretamente).