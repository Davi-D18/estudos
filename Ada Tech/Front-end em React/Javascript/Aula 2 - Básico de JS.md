## Booleanos em Javascript

Em Javascript, um Booleano é um tipo de dado que possui apenas dois valores possíveis: `true` (verdadeiro) ou `false` (falso). Booleanos são comumente usados em testes condicionais.

Exemplo:

```jsx
let teste = true;

```

## Condicional if

O comando `if` é usado em Javascript para realizar um teste condicional. Se a condição entre parênteses for verdadeira (`true`), o bloco de código dentro das chaves `{}` será executado.

Exemplo:

```jsx
let numero = 10;
if (numero > 5) {
  console.log("O número é maior que 5");
}

```

## Condicional if...else

Você pode usar a declaração `else` com a declaração `if` para executar um bloco de código se a condição for falsa.

Exemplo:

```jsx
let numero = 4;
if (numero > 5) {
  console.log("O número é maior que 5");
} else {
  console.log("O número é menor ou igual a 5");
}

```

## JavaScript básico - Outros tópicos importantes

Além dos booleanos e condicionais, existem outros tópicos importantes no Javascript básico que você deve revisar:

## Variáveis e tipos de dados

### Variáveis e tipos de dados

Variáveis em Javascript podem armazenar diferentes tipos de dados. Os tipos de dados mais comuns são `number`, `string`, `boolean`, `object` e `undefined`.

Exemplo:

```jsx
let numero = 10;    // number
let nome = 'João';  // string
let teste = true;   // boolean
let pessoa = {};    // object
let nada;           // undefined

```

## Operadores

### Operadores

Os operadores são usados para realizar operações entre variáveis e valores. Os operadores mais comuns são aritméticos (como `+`, `-`, `*`, `/`), de comparação (como `==`, `!=`, `<`, `>`), lógicos (como `&&`, `||`, `!`) e de atribuição (como `=`, `+=`, `-=`, `*=`).

Exemplo:

```jsx
let x = 5;
let y = 10;
let z = x + y;    // z será 15

```

Os operadores de comparação em JavaScript são usados para comparar dois valores.

- `==` (Igual a): testa se dois valores são iguais, independentemente do tipo.
- `===` (Estritamente igual a): testa se dois valores são iguais e do mesmo tipo.
- `!=` (Diferente de): testa se dois valores são diferentes.
- `!==` (Estritamente diferente de): testa se dois valores são diferentes ou se não são do mesmo tipo.
- `<` (Menor que): testa se um valor é menor que outro.
- `>` (Maior que): testa se um valor é maior que outro.
- `<=` (Menor ou igual a): testa se um valor é menor ou igual a outro.
- `>=` (Maior ou igual a): testa se um valor é maior ou igual a outro.

Exemplo:

```jsx
let x = 5;
let y = "5";

console.log(x == y);  // Retorna true, porque os valores são iguais
console.log(x === y); // Retorna false, porque os tipos são diferentes

```

## Operadores lógicos

Os operadores lógicos são usados para determinar a lógica entre variáveis ou valores. Aqui estão os operadores lógicos mais comuns:

- `&&` (E): retorna verdadeiro se ambos os operandos forem verdadeiros.
- `||` (OU): retorna verdadeiro se qualquer um dos operandos for verdadeiro.
- `!` (NÃO): retorna verdadeiro para falso e falso para verdadeiro.

Exemplo:

```jsx
let a = 5;
let b = 10;
let c = 15;

console.log(a < b && b < c); // Retorna true, porque ambas as condições são verdadeiras

```

## Operadores de atribuição

Os operadores de atribuição são usados para atribuir valores a variáveis. Aqui estão os operadores de atribuição mais comuns:

- `=`: atribui um valor a uma variável.
- `+=`: adiciona um valor a uma variável.
- `=`: subtrai um valor de uma variável.
- `=`: multiplica uma variável.
- `/=`: divide uma variável.
- `%=`: atribui um resto a uma variável.

Exemplo:

```jsx
let a = 10;

a += 5;  // a agora é 15
a -= 3;  // a agora é 12
a *= 2;  // a agora é 24
a /= 4;  // a agora é 6
a %= 2;  // a agora é 0

```

Outro operador de atribuição importante é o operador de atribuição de desestruturação `=` que permite desempacotar valores de arrays ou propriedades de objetos em variáveis distintas.

Exemplo:

```jsx
let [a, b] = [1, 2];  // a agora é 1 e b é 2
let {x, y} = {x: 5, y: 10};  // x agora é 5 e y é 10

```

## Loops (for, while)

### Loops (for, while)

Loops são usados para executar um blobo de código várias vezes. Os mais comuns são `for` e `while`.

Exemplo:

```jsx
for (let i = 0; i < 5; i++) {
  console.log(i);  // irá imprimir 0, 1, 2, 3, 4
}

```

## Funções

### Funções

Funções são blocos de código que podem ser definidos e chamados pelo nome.

Exemplo:

```jsx
function saudacao(nome) {
  console.log('Olá, ' + nome);
}
saudacao('João');  // irá imprimir "Olá, João"

```

## Arrays

### Arrays

Arrays são usados para armazenar vários valores em uma única variável.

Exemplo:

```jsx
let frutas = ['maçã', 'banana', 'laranja'];
console.log(frutas[0]);  // irá imprimir "maçã"

```

## Objetos

### Objetos

Objetos são uma coleção de propriedades. As propriedades são definidas como pares de nome/valor.

Exemplo:

```jsx
let pessoa = {
  nome: 'João',
  idade: 30,
  cidade: 'São Paulo'
};
console.log(pessoa.nome);  // irá imprimir "João"

```

## Switch Case

## Switch Case

O comando `switch` é usado para selecionar um dos muitos blocos de código para ser executado. É uma maneira alternativa para expressar uma sequência complexa de `if...else if...else`.

A expressão dentro do comando `switch` é avaliada uma vez. O valor da expressão é comparado com os valores de cada caso (`case`). Se houver correspondência, o bloco de código associado é executado.

Exemplo:

```jsx
let fruta = 'maçã';

switch (fruta) {
  case 'banana':
    console.log('Eu sou uma banana');
    break;
  case 'maçã':
    console.log('Eu sou uma maçã');
    break;
  default:
    console.log('Eu não sou nem uma banana nem uma maçã');
}
// 'Eu sou uma maçã' será impresso, pois a variável fruta contém o valor 'maçã'

```

Nota:

- `break`: Quando JavaScript encontra um `break` ele sai do bloco `switch`. Isso impedirá a execução inadvertida de blocos de código que vêm depois do bloco correspondente.
- `default`: Define o bloco de código a ser executado se não houver correspondência em nenhum dos casos.

## Mais detalhes sobre Switch Case

### Uso de `break`

A instrução `break` é importante quando usamos o `switch`. Sem ela, se um caso corresponder, todos os casos subsequentes serão executados até encontrar um `break`, mesmo que não correspondam à condição.

```jsx
let fruta = 'maçã';

switch (fruta) {
  case 'banana':
    console.log('Eu sou uma banana');
    break;
  case 'maçã':
    console.log('Eu sou uma maçã');
    // Sem o 'break' aqui, o próximo caso será executado
  case 'laranja':
    console.log('Eu sou uma laranja');
    break;
  default:
    console.log('Eu não sou nem uma banana nem uma maçã nem uma laranja');
}
// 'Eu sou uma maçã' e 'Eu sou uma laranja' serão impressos

```

### Uso do `default`

O `default` é opcional e pode ser usado no final do `switch` para capturar todos os casos que não correspondem a nenhum dos casos listados. Se o `default` for omitido e nenhum caso corresponder, nenhum bloco de código será executado.

```jsx
let fruta = 'pera';

switch (fruta) {
  case 'banana':
    console.log('Eu sou uma banana');
    break;
  case 'maçã':
    console.log('Eu sou uma maçã');
    break;
  // Sem o 'default', nada será impresso se fruta não for 'banana' nem 'maçã'
}

```

### Ordem dos casos

A ordem dos casos no `switch` é importante. Os casos são testados de cima para baixo, por isso, o primeiro caso que corresponder será executado.

```jsx
let numero = 5;

switch (numero) {
  case 1:
    console.log('O número é 1');
    break;
  case 5:
    console.log('O número é 5');
    break;
  case 10:
    console.log('O número é 10');
    break;
  default:
    console.log('O número não é 1, 5 nem 10');
}
// 'O número é 5' será impresso

```

### Comparação estrita

O `switch` usa a comparação estrita (`===`), o que significa que o tipo de dado também é levado em conta.

```jsx
let valor = '5';

switch (valor) {
  case 5:
    console.log('O valor é 5');
    break;
  default:
    console.log('O valor não é 5');
}
// 'O valor não é 5' será impresso, pois estamos comparando uma string com um número

```

## Operador Térnario

### Operador Ternário

O operador ternário é uma forma compacta de escrever uma instrução condicional. Ele é chamado de "ternário" porque envolve três operandos. A sintaxe é `condição ? expressãoSeVerdadeira : expressãoSeFalsa`.

Por exemplo, vamos supor que temos uma variável chamada `idade` e queremos determinar se a pessoa é maior de idade:

```jsx
let idade = 20;
let maiorIdade = (idade >= 18) ? "Sim" : "Não";
console.log(maiorIdade); // Irá imprimir "Sim"

```

Neste exemplo, se a condição `idade >= 18` for verdadeira, a expressão após o `?` ("Sim") será o valor de `maiorIdade`. Se for falsa, a expressão após o `:` ("Não") será o valor de `maiorIdade`.

### Mais Exemplos de Uso do Operador Ternário

O operador ternário também pode ser usado para fazer escolhas rápidas baseadas em condições. Por exemplo, você pode usá-lo para decidir o que imprimir na tela com base no valor de uma variável.

```jsx
let numero = 10;
console.log((numero > 5) ? "O número é maior que 5" : "O número é menor ou igual a 5");
// Irá imprimir "O número é maior que 5"

```

Neste exemplo, se a condição `numero > 5` for verdadeira, a expressão "O número é maior que 5" será impressa. Caso contrário, "O número é menor ou igual a 5" será impresso.

O operador ternário pode ser usado mais de uma vez na mesma linha para avaliar múltiplas condições. Por exemplo:

```jsx
let idade = 20;
let situacao = (idade < 18) ? "Menor de idade" : (idade < 60) ? "Adulto" : "Idoso";
console.log(situacao); // Irá imprimir "Adulto"

```

Neste exemplo, temos três condições. Se `idade < 18` for verdadeira, a expressão "Menor de idade" será o valor de `situacao`. Se for falsa, a próxima condição `idade < 60` será avaliada. Se essa condição for verdadeira, a expressão "Adulto" será o valor de `situacao`. Se ambas as condições forem falsas, a expressão "Idoso" será o valor de `situacao`.

Lembre-se de que o operador ternário é útil para simplificar o código, mas também pode tornar o código mais difícil de ler se usado em excesso ou com condições muito complexas.

## Truthy e Falsy

Em JavaScript, os valores truthy e falsy são conceitos importantes que se referem a quais valores são considerados verdadeiros ou falsos em contextos booleanos.

### Valores Falsy

Os valores falsy são aqueles que são considerados falsos quando encontrados em um contexto booleano. JavaScript considera os seguintes valores como falsy:

- `false`
- `0` (zero)
- `''` ou `""` (string vazia)
- `null`
- `undefined`
- `NaN` (Not a Number)

### Valores Truthy

Os valores truthy são aqueles que são considerados verdadeiros quando encontrados em um contexto booleano. Em JavaScript, todos os valores são truthy a menos que sejam definidos como falsy.

Isso significa que se você pegar um valor que não esteja na lista de valores falsy, ele será considerado truthy. Por exemplo, objetos vazios `{}` e arrays vazios `[]` são truthy, assim como strings não vazias e números diferentes de zero.

### Exemplos de uso:

```jsx
if (0) {
  console.log("0 é truthy");
} else {
  console.log("0 é falsy");
}
// Isto irá imprimir "0 é falsy"

if ("Olá") {
  console.log("'Olá' é truthy");
} else {
  console.log("'Olá' é falsy");
}
// Isto irá imprimir "'Olá' é truthy"

if ({}) {
  console.log("{} é truthy");
} else {
  console.log("{} é falsy");
}
// Isto irá imprimir "{} é truthy"

```

Entender os conceitos de truthy e falsy é fundamental para entender a lógica em JavaScript, especialmente ao trabalhar com instruções condicionais e loops.