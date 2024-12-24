Em PHP, para facilitar a organização do código, você pode dividir sua aplicação em vários arquivos e **importar** esses arquivos sempre que necessário. Isso é feito com as instruções `require`, `include`, `require_once` e `include_once`. Essas instruções são usadas para carregar o conteúdo de um arquivo em outro. Vamos entender as diferenças e como usá-las.

---

### **1. `require`**

- **Função**: Importa o conteúdo de outro arquivo PHP.
- **Comportamento**: Se o arquivo não for encontrado ou tiver erros, o PHP **interrompe a execução do script** (lança um erro fatal).
- **Quando usar**: Para arquivos **essenciais**, sem os quais o script não deve continuar.

**Exemplo**:

```php
// arquivo1.php 
<?php 
	echo "Olá do arquivo1!"; 
?>  // arquivo_principal.php 

<?php 
	require 'arquivo1.php'; // Importa arquivo1.php 
	echo "Isso será exibido após o arquivo1 ser incluído."; 
?>
```

**Se o arquivo não existir**:

```php
<?php 
	require 'inexistente.php'; // Erro fatal: o script será interrompido
	echo "Isso nunca será exibido."; 
?>
```

---

### **2. `include`**

- **Função**: Também importa o conteúdo de outro arquivo PHP.
- **Comportamento**: Se o arquivo não for encontrado, o PHP lança um **aviso (warning)**, mas o script continua a execução.
- **Quando usar**: Para arquivos que **não são críticos** para o funcionamento do script.

```php
// arquivo_opcional.php
<?php
	echo "Arquivo opcional carregado!";
?>

// arquivo_principal.php
<?php
	include 'arquivo_opcional.php'; // Importa o arquivo opcional
	echo "O script continua mesmo que o arquivo não seja encontrado.";
?>

```

**Se o arquivo não existir**:

```php
<?php
	include 'inexistente.php'; // Apenas um aviso, o script continua
	echo "Isso será exibido, apesar do erro.";
?>

```

---

### **3. `require_once`**

- **Função**: Igual ao `require`, mas garante que o arquivo será importado **somente uma vez**, mesmo que a instrução seja chamada várias vezes.
- **Quando usar**: Quando você quer evitar **duplicação de código** ao carregar o mesmo arquivo.

**Exemplo**:

```php
// configuracao.php
<?php
	echo "Configurações carregadas!";
?>

// arquivo_principal.php
<?php
	require_once 'configuracao.php'; // Carrega o arquivo pela primeira vez
	require_once 'configuracao.php'; // Não será carregado novamente
?>

```

---

### **4. `include_once`**

- **Função**: Igual ao `include`, mas garante que o arquivo será importado **somente uma vez**, mesmo que chamado múltiplas vezes.
- **Quando usar**: Para arquivos não críticos que você não quer carregar mais de uma vez.

**Exemplo**:

```php
// funcoes.php
<?php
	echo "Funções carregadas!";
?>

// arquivo_principal.php
<?php
	include_once 'funcoes.php'; // Carregado uma vez
	include_once 'funcoes.php'; // Ignorado na segunda vez
?>

```

---

### **Diferenças Resumidas**

| Instrução  | Erro ao Não Encontrar Arquivo | Importa Mais de Uma Vez? | Uso Recomendado                    |
| -------------- | --------------------------------- | ---------------------------- | -------------------------------------- |
| `require`      | Fatal Error                       | Sim                          | Arquivos essenciais                    |
| `include`      | Warning                           | Sim                          | Arquivos opcionais                     |
| `require_once` | Fatal Error                       | Não                          | Arquivos essenciais, evitar duplicação |
| `include_once` | Warning                           | Não                          | Arquivos opcionais, evitar duplicação  |

---

### **Boa Prática**

- Sempre que um arquivo conter **funções** ou **configurações globais**, use `require_once` ou `include_once` para evitar problemas de **duplicação**.
- Para **dependências críticas**, prefira `require`.
- Para **dependências opcionais**, use `include`.

---

### **Exemplo Completo**

```php
// config.php
<?php
	echo "Configuração carregada!";
?>

// funcoes.php
<?php
function ola() {
    echo "Olá, mundo!";
}
?>

// principal.php
<?php
	require_once 'config.php'; // Garante que será carregado apenas uma vez
	include 'funcoes.php';    // Carrega funções
	include 'funcoes.php';    // Não há problema em carregar de novo, mas pode ser redundante

	ola(); // Chama a função definida no arquivo funcoes.php
?>

```