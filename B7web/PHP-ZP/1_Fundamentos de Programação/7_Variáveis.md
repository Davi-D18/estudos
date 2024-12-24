#### **1. O que são Variáveis Globais em PHP?**

- **Definição**: Variáveis globais são acessíveis em todo o escopo de um script, mas para usá-las dentro de funções ou métodos, é necessário declará-las explicitamente como `global`.
- **Uso típico**: Em projetos menores, variáveis globais são usadas para armazenar configurações ou dados compartilhados. Contudo, em projetos grandes, o uso excessivo deve ser evitado.

**Exemplo Simples:**

```php
<?php
$nome = "Luiz Davi"; // Variável global

function exibirNome() {
    global $nome; // Declaração explícita como global
    echo $nome;
}

exibirNome(); // Saída: Luiz Davi
?>

```

---

#### **2. Superglobais no PHP**

- São variáveis globais **pré-definidas** disponíveis em todos os escopos sem necessidade de declaração explícita.
- Exemplos:
    - `$_GET` - Dados da URL (query string).
    - `$_POST` - Dados enviados via formulário HTTP POST.
    - `$_SESSION` - Dados da sessão atual.
    - `$_COOKIE` - Dados armazenados nos cookies.

**Exemplo com Superglobal:**

```php
<?php
$_GET['id'] = 10;

echo "O ID passado é: " . $_GET['id']; // Saída: O ID passado é: 10
?>

```

---

#### **3. Constantes em PHP**

- **Definição**: Uma constante é um identificador (nome) para um valor único e imutável durante a execução do script.
- **Definição de Constantes**:
    - Usa-se a função `define()` em PHP 7.
    - Desde PHP 7.0, é possível usar a palavra-chave `const` fora de classes para definição mais legível.

**Sintaxe e Exemplos:**

```php
<?php
// Definindo constante com define()
define("APP_NAME", "Sistema HidroInova");

// Definindo constante com const (PHP 7+)
const VERSAO = "1.0";

// Exibindo constantes
echo APP_NAME; // Saída: Sistema HidroInova
echo VERSAO;   // Saída: 1.0
?>

```

- **No PHP 8**, o uso de constantes permanece o mesmo.

---

#### **4. Diferenças Importantes nas Versões 7 e 8**

- **Variáveis Globais e Superglobais**:
    - Não houve mudanças significativas entre PHP 7 e 8.
    - No PHP 8, os warnings ao acessar variáveis não definidas podem ser mais explícitos (ajudando no debugging).
- **Constantes**:
    - No PHP 7 e 8, as constantes definidas com `const` podem ser usadas em escopos locais e globais.
    - O PHP 8 trouxe melhorias de tipagem, tornando o código mais seguro (especialmente ao usar constantes em expressões).

---

#### **5. Usando Variáveis Globais e Constantes Juntas**

- É comum usar constantes para armazenar valores fixos (ex: configurações) e variáveis globais para dados que mudam.

**Exemplo Prático:**

```php
<?php
define("URL_BASE", "https://meusite.com");

// Variável global
$usuarioAtual = "admin";

function gerarLinkPerfil() {
    global $usuarioAtual; // Tornando a variável global acessível
    return URL_BASE . "/usuario/" . $usuarioAtual;
}

echo gerarLinkPerfil(); // Saída: https://meusite.com/usuario/admin
?>

```

---

#### **6. Boas Práticas**

1. **Minimize o uso de variáveis globais**:
    
    - Prefira usar escopos locais ou passar variáveis como parâmetros para funções.
    - Use superglobais para manipular dados de entrada, como `$_POST` e `$_GET`.
2. **Centralize constantes em um arquivo dedicado**:
    
    - Exemplo: `config.php` para definir valores fixos, como URLs e credenciais de banco de dados.
3. **Atualize para PHP 8 se possível**:
    
    - A versão 8 oferece recursos como tipagem aprimorada e melhor performance.
4. **Documente suas variáveis e constantes**:
    
    - Mantenha comentários explicando o propósito de cada uma, para facilitar a manutenção.

---

#### **Resumo**

- **Variáveis Globais**: Precisam ser declaradas explicitamente com `global` em funções.
- **Superglobais**: Pré-definidas e disponíveis em todo o script.
- **Constantes**: Valores fixos e imutáveis, definidos com `define()` ou `const`.
- **Diferenças PHP 7 e 8**: Constantes e variáveis globais permanecem consistentes entre versões, com pequenas melhorias de debugging no PHP 8.

### **Diferenças entre Variáveis Globais e Constantes**

| Característica        | Variáveis Globais           | Constantes                                  |
| ------------------------- | ------------------------------- | ----------------------------------------------- |
| **Mutabilidade**          | Podem mudar de valor            | Não podem ser alteradas após definidas          |
| **Como declarar**         | `$variavel = valor;`            | `define("NOME", valor);`                        |
| **Uso dentro de funções** | Requer a palavra-chave `global` | Acessível diretamente (não precisa de `global`) |
| **Valor fixo?**           | Não, pode ser alterado          | Sim, o valor é fixo                             |
Exemplo:
```php
<?php
// Variável global
$usuarioAtual = "Admin";

// Constante
define("APP_NOME", "HidroInova");

function exibirInformacoes() {
    global $usuarioAtual; // Tornar a variável global acessível na função
    echo "Usuário: $usuarioAtual, Aplicativo: " . APP_NOME;
}

exibirInformacoes(); // Saída: Usuário: Admin, Aplicativo: HidroInova
?>

```