### Comentários no PHP:

- **Linha única**: Use `//` ou `#`
- **Bloco de múltiplas linhas**: Use `/* ... */`

Exemplo:

```php
<?php     
	// Este é um comentário de uma linha     
	# Este também é um comentário de uma linha     
	/* Este é um comentário de várias linhas     */ 
?>
```

---

## 3. Variáveis

- As variáveis no PHP começam com `$`.
- Não precisam ser declaradas explicitamente.
- São tipadas dinamicamente (não precisa especificar o tipo).

### Exemplos:

```php
<?php     
	$nome = "Luiz"; // String     
	$idade = 20; // Inteiro     
	$altura = 1.75; // Float     
	$casado = false; // Booleano      
	echo "Nome: $nome, Idade: $idade anos"; 
?>
```

### Regras para nomes de variáveis:

1. Devem começar com `$`.
2. Não podem começar com números.
3. Não podem conter espaços.

---

## 4. Tipos de Dados

### Principais tipos:

- **String**: Texto.
- **Integer**: Números inteiros.
- **Float**: Números decimais.
- **Boolean**: Verdadeiro (`true`) ou Falso (`false`).
- **Array**: Conjunto de valores.
- **Object**: Representação de objetos (POO).
- **NULL**: Representa uma variável sem valor.

---

## 5. Strings

### Trabalhando com Strings:

```php
<?php     
	$nome = "Luiz";
	      
	// Concatenação 
	    
	echo "Olá, " . $nome . "!";
	      
	// Aspas simples vs duplas 
	
	echo 'Olá, $nome!'; // Exibe: Olá, $nome!  
	   
	echo "Olá, $nome!"; // Exibe: Olá, Luiz!
	      
	// Funções úteis     
	echo strlen("Texto"); 
	
	// Comprimento da string     
	echo str_replace("mundo", "PHP", "Olá, mundo!"); // Substitui texto 
?>
```

---

## 6. Constantes

As constantes são variáveis imutáveis durante a execução do script.


```php
<?php     
	define("VERSAO", "1.0");     
	echo VERSAO; // Exibe: 1.0 
?>
```

---

## 7. Operadores

### Aritméticos:

```php
<?php     
	$a = 10;     
	$b = 3;      
	echo $a + $b; // Soma     
	echo $a - $b; // Subtração     
	echo $a * $b; // Multiplicação     
	echo $a / $b; // Divisão     
	echo $a % $b; // Módulo 
?>
```

### Comparação:

```php
<?php     
	$a = 10;     
	$b = 20;      
	echo $a == $b; // Igual     
	echo $a != $b; // Diferente     
	
	echo $a > $b; // Maior que     
	echo $a < $b; // Menor que 
?>
```

---

## 8. Estruturas de Controle

### Condicional `if-else`:

```php
<?php     
	$idade = 18;      
	if ($idade >= 18) {         
		echo "Você é maior de idade.";     
	} else {         
		echo "Você é menor de idade.";     
	} 
?>
```

### Condicional `switch`:

```php
<?php     
	$cor = "vermelho";      
	switch ($cor) {         
	case "azul":             
		echo "A cor é azul.";             
		break;         
	case "vermelho":             
		echo "A cor é vermelho.";             
		break;         
	default:             
		echo "Cor não identificada.";     
	} 
?>```

---

## 9. Arrays

### Array Simples:

```php
<?php     
	$frutas = ["Maçã", "Banana", "Uva"];     
	echo $frutas[0]; // Maçã 
?>
```

### Array Associativo:

```php
<?php     
	$pessoa = ["nome" => "Luiz", "idade" => 20];     
	echo $pessoa["nome"]; // Luiz 
?>
```

### Laços com Arrays:

```php
<?php     
	$frutas = ["Maçã", "Banana", "Uva"];      
	foreach ($frutas as $fruta) {         
		echo $fruta . "<br>";     
	} 
?>
```

---

## 10. Funções

As funções ajudam a organizar o código e reaproveitar lógica.

### Exemplo de Função:

```php
<?php     
	function saudacao($nome) {         
		return "Olá, $nome!";     
	}      
	
	echo saudacao("Luiz"); // Olá, Luiz! 
?>
```

---

## 11. Trabalhando com Formulários

PHP é ótimo para processar formulários HTML.

### Exemplo:

#### Arquivo `form.html`:

```html
<form action="processar.php" method="POST">     
	<label for="nome">Nome:</label>     
	<input type="text" id="nome" name="nome">     
	<button type="submit">Enviar</button> 
</form>
```

#### Arquivo `processar.php`:

```php
<?php     
	$nome = $_POST['nome'];     
	echo "Você enviou o nome: $nome"; 
?>
```

---

## 12. Validação de Formulários

Sempre valide entradas para evitar problemas como SQL Injection.

```php
<?php     
	if ($_SERVER["REQUEST_METHOD"] == "POST") {         
		$nome = htmlspecialchars($_POST['nome']); // Remove caracteres perigosos
		echo "Nome válido: $nome";     
	} 
?>
```

---

## 13. Conexão com Banco de Dados

### Conectando ao Banco:

```php
<?php     
	$conn = new mysqli("localhost", "root", "", "meu_banco");      
	if ($conn->connect_error) {         
		die("Erro de conexão: " . $conn->connect_error);     
	}      
	echo "Conexão bem-sucedida!"; 
?>
```

### Executando uma Query:

```php
<?php     
	$sql = "SELECT * FROM usuarios";     
	$result = $conn->query($sql);      
	if ($result->num_rows > 0) {         
		while ($row = $result->fetch_assoc()) {             
			echo "Nome: " . $row["nome"] . "<br>";         
		}     
	} 
	else {         
		echo "Nenhum resultado encontrado.";     
	} 
?>
```

# Array Multidimensional  
Um **array multidimensional** é simplesmente um array que contém outros arrays como elementos. Em PHP, esse tipo de estrutura de dados é muito útil quando você precisa armazenar informações relacionadas de forma organizada, como uma lista de produtos, alunos, ou outros conjuntos de dados estruturados.

- **Array Principal: `$produtos`** O array `$produtos` é o **array principal**. Ele contém **outros arrays** dentro de si. Esses arrays internos podem ser de diferentes tipos, como arrays associativos (onde as chaves são strings), ou simples arrays indexados.
    
- **Arrays Internos** Cada elemento dentro do array principal pode ser um **array associativo**. Em um array associativo, em vez de usar índices numéricos (como 0, 1, 2), você utiliza **chaves associativas** para acessar os dados, como `"nome"`, `"quantidade"`, e `"infor"`.

```php
<?php
	array( "nome" => "1", // Chave "nome" com valor "1" 
		"quantidade" => "", // Chave "quantidade" vazia 
		"infor" => "" // Chave "infor" vazia 
	)
?>
```

#### 3. **Estrutura do Código**

O array `$produtos` pode ter vários arrays associativos internos. Veja o exemplo do código:

```php
	$produtos = array(     
		array("nome" => "1", "quantidade" => "", "infor" => ""),
		array("nome" => "2", "quantidade" => "", "infor" => "") 
	);
```

Aqui, o array `$produtos` contém **dois produtos**, cada um representado por um array associativo. O **índice 0** refere-se ao primeiro produto, e o **índice 1** ao segundo. Além disso, um novo produto pode ser adicionado dinamicamente usando a sintaxe:

```php
	$produtos[] = array(     
		"nome" => "3",     
		"quantidade" => "",     
		"infor" => "" 
	);
```

O operador `[]` adiciona o array à próxima posição disponível do array principal, automaticamente.

**Representação visual** do array `$produtos`:

|Índice|Nome|Quantidade|Infor|
|---|---|---|---|
|0|1|(vazio)|(vazio)|
|1|2|(vazio)|(vazio)|
|2|3|(vazio)|(vazio)|

#### 4. **Acessando os Dados**

Para acessar os dados dentro de um array multidimensional, você usa o **índice do array principal** e a **chave associativa** do array interno. Por exemplo:

- Para acessar o **nome** do primeiro produto:

```php
	echo $produtos[0]["nome"];  // Resultado: 1
```

- Para acessar a **quantidade** do terceiro produto (índice 2):

```php
	echo $produtos[2]["quantidade"];  // Resultado: (vazio)
```

No exemplo acima, `$produtos[0]["nome"]` retorna "1", pois acessamos o primeiro array dentro de `$produtos` e pegamos o valor associado à chave `"nome"`.

#### 5. **Usos Práticos**

Arrays multidimensionais são extremamente úteis em várias situações, como:

- **Lista de produtos**: Para armazenar informações detalhadas sobre cada produto, como nome, preço, quantidade em estoque, etc.
- **Cadastro de alunos**: Onde cada aluno tem várias informações (nome, idade, notas).
- **Dados estruturados de APIs**: Quando você recebe uma resposta de uma API com dados organizados em várias categorias.

```php
$alunos = array(     
	array("nome" => "João", "idade" => 20, "nota" => 8.5),     
	array("nome" => "Maria", "idade" => 22, "nota" => 9.0) 
);
```

### Conclusão

Em resumo, um **array multidimensional** em PHP é uma poderosa ferramenta para organizar dados estruturados. Você pode acessar dados através de índices e chaves associativas, tornando a manipulação de grandes volumes de dados mais eficiente e fácil de entender. Esses arrays são essenciais em muitos cenários, como gerenciamento de produtos, usuários ou outros tipos de informações estruturadas.