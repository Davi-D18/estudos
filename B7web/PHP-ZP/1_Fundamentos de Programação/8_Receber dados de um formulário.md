![[Pasted image 20241123104144.png]]

1. **`$_POST`:**
    
    - É uma superglobal em PHP usada para coletar dados enviados via o método `POST` de um formulário HTML.
    - No exemplo, os valores dos campos "email" e "senha" são acessados por meio de `$_POST['email']` e `$_POST['senha']`.
2. **`isset()`:**
    
    - Verifica se uma variável foi definida e não é `null`.
    - Aqui, `isset($_POST['email'])` garante que o campo "email" foi enviado no formulário.
3. **`empty()`:**
    
    - Retorna `true` se o valor fornecido for vazio, como uma string vazia (`""`), `0`, `null`, ou uma variável não definida.
    - `empty($_POST['email'])` verifica se o campo "email" está vazio.
4. **Operador lógico `&&`:**
    
    - É usado para combinar condições. Ambas as condições precisam ser verdadeiras para que o bloco de código seja executado.
    - No código, `isset($_POST['email']) && empty($_POST['email'])` verifica se o campo "email" foi enviado e está vazio.
5. **`echo`:**
    
    - Exibe uma saída no navegador.
    - Aqui, ele mostra a mensagem "O usuario enviou os dados" se as condições forem atendidas.
6. **`<form method="POST">`:**
    
    - Define um formulário HTML que enviará dados usando o método `POST`.
7. **Inputs:**
    
    - `<input type="text" name="email" />`: Campo de texto para o usuário inserir o e-mail.
    - `<input type="password" name="senha" />`: Campo de senha.
    - `<input type="submit" value="Enviar Dados" />`: Botão para enviar o formulário.

---

### Anotações para estudo

#### **Superglobais em PHP**

- **`$_POST`:** Recebe dados enviados via método `POST`.
- **`$_GET`:** Recebe dados enviados via método `GET`.

---

#### **Funções importantes**

- **`isset($var)`:** Retorna `true` se a variável for definida e diferente de `null`.
- **`empty($var)`:** Retorna `true` se a variável for vazia (`""`, `0`, `null`, etc.).
- **`echo`:** Imprime textos ou valores no navegador.

---

#### **Formulário em HTML**

- Use `method="POST"` para enviar dados com segurança.
- Campos comuns:
    - `type="text"`: Entrada de texto.
    - `type="password"`: Campo para senhas.
    - `type="submit"`: Botão de envio.


**Validação dos Dados:**

- É importante validar os dados antes de usá-los, para evitar problemas de segurança.
- Funções comuns de validação:
    - `isset($var)`: Verifica se uma variável foi enviada.
    - `empty($var)`: Verifica se uma variável está vazia.
    - `filter_var($var, FILTER_VALIDATE_EMAIL)`: Valida e-mails

```php
<?php
if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    $email = $_POST['email'];
    $senha = $_POST['senha'];

    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        echo "E-mail inválido.";
    } elseif (empty($senha)) {
        echo "A senha não pode estar vazia.";
    } else {
        echo "Dados recebidos com sucesso!";
    }
}
?>

```

### **Explicação do Código**

1. **`if ($_SERVER['REQUEST_METHOD'] === 'POST')`:**
    - Verifica se o formulário foi enviado usando o método `POST`.
    - Essa validação garante que o código só será executado se houver envio de dados pelo formulário.

---

2. **`$email = $_POST['email'];` e `$senha = $_POST['senha'];`:**
    - Essas linhas capturam os valores enviados nos campos do formulário (com os `name="email"` e `name="senha"`).
    - `$email` armazenará o valor digitado no campo de e-mail.
    - `$senha` armazenará o valor digitado no campo de senha.

---

3. **`if (!filter_var($email, FILTER_VALIDATE_EMAIL))`:**
    - Aqui, o código valida se o e-mail fornecido pelo usuário é válido.
    - A função `filter_var()` com o filtro `FILTER_VALIDATE_EMAIL` verifica o formato do e-mail.
    - Se o e-mail for inválido, exibe a mensagem **"E-mail inválido."**.

---

4. **`elseif (empty($senha))`:**
    - Verifica se o campo da senha está vazio.
    - A função `empty()` retorna `true` se `$senha` for uma string vazia (`""`), `null`, ou `0`.
    - Se o campo estiver vazio, exibe a mensagem **"A senha não pode estar vazia."**.

---

5. **`else { echo "Dados recebidos com sucesso!"; }`:**
    - Caso o e-mail seja válido e a senha não esteja vazia, essa mensagem é exibida.
    - Isso indica que os dados passaram pelas validações.

---

### **Fluxo do Código**

1. O código espera o envio do formulário via `POST`.
2. Após o envio:
    - Verifica o formato do e-mail.
    - Verifica se o campo da senha foi preenchido.
3. Exibe mensagens de validação apropriadas:
    - **E-mail inválido** → Formato do e-mail errado.
    - **Senha vazia** → O usuário não digitou uma senha.
    - **Dados recebidos com sucesso!** → Tudo está correto.

---

### **Exemplo Prático**

Imagine o seguinte formulário HTML conectado a esse código PHP:

```html
<form action="processa.php" method="POST">
    <label for="email">E-mail:</label>
    <input type="text" id="email" name="email" required>
    
    <label for="senha">Senha:</label>
    <input type="password" id="senha" name="senha" required>
    
    <button type="submit">Enviar</button>
</form>
```


#### Cenários possíveis:

- **Usuário digita um e-mail inválido (`exemplo@com`):**
    - Saída: **"E-mail inválido."**
- **Usuário não preenche a senha:**
    - Saída: **"A senha não pode estar vazia."**
- **Usuário preenche tudo corretamente:**
    - Saída: **"Dados recebidos com sucesso!"**

---

### **Dicas Adicionais**

- Sempre valide os dados recebidos do usuário para evitar erros e vulnerabilidades de segurança.
- Personalize as mensagens de erro para uma melhor experiência do usuário.
- Para sistemas mais complexos, armazene os dados recebidos em um banco de dados (por exemplo, MySQL).