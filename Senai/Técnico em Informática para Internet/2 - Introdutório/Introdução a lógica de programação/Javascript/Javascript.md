---
Criado: Data inválida
Tipo: Aula
Materiais:
  - https://github.com/Davi-D18/Senai/tree/main/L%C3%B3gica_de_programa%C3%A7%C3%A3o/javascript
Revisado: Não iniciada
Inicio: Data inválida
Matéria: Lógica de Programação
Última edição: Data inválida
---
## Operadores

### Aritméticos

![[GetImage_(6).png]]

### Atribuição

**1. O Essencial: Atribuindo Valores**

- `=`: Atribui um valor à variável à esquerda, vindo da expressão à direita.
- Exemplo: `x = 10; // x agora armazena 10`

**2. Operadores Combinados: Fazendo Mais com Menos**

- `+=`: Adiciona e atribui na mesma operação.
    - Exemplo: `x += 5; // x agora é 15 (x + 5)`
- `=`: Subtrai e atribui na mesma operação.
    - Exemplo: `y -= 3; // y agora é 7 (y - 3)`
- `=`: Multiplica e atribui na mesma operação.
    - Exemplo: `z *= 2; // z agora é 20 (z * 2)`
- `/=`: Divide e atribui na mesma operação.
    - Exemplo: `w /= 4; // w agora é 2.5 (w / 4)`
- `%=`: Obtém o resto da divisão e atribui.
    - Exemplo: `n %= 6; // n agora é 0 (resto de n dividido por 6)`

**3. Cópia vs. Referência: Entendendo as Diferenças**

- **Cópia:** Cria um novo valor com base no original, mas independente na memória.
    - Exemplo: `const numeros = [1, 2, 3]; const outrosNumeros = [...numeros]; // 'outrosNumeros' é uma cópia de 'numeros' com memória própria`
- **Referência:** Cria um apelido para um valor já armazenado na memória.
    - Exemplo: `const pessoa = { nome: 'João' }; const outraPessoa = pessoa; // 'outraPessoa' agora referencia o mesmo objeto que 'pessoa'`

**4. Lidando com Valores Indefinidos com Segurança**

- `??=`: Atribui um valor padrão se o valor à direita for `null` ou `undefined`.
    - Exemplo: `const cidade = usuario?.cidade ?? 'Brasília'; // 'cidade' recebe 'Brasília' se 'usuario.cidade' for null ou undefined`
- `||=`: Atribui o valor à direita se o valor à esquerda for `falsy` (falso).
    - Exemplo: `const nomeCompleto = nome || sobrenome; // 'nomeCompleto' recebe 'nome' se definido, caso contrário recebe 'sobrenome'`

**5. Operadores Avançados para Atribuições Complexas**

- **Atribuição Desestruturante:** Extrai propriedades de objetos e arrays para várias variáveis de forma concisa.
    - Exemplo: `const [primeiro, segundo] = [10, 20]; // 'primeiro' armazena 10 e 'segundo' armazena 20`
- **Atribuição de Troca:** Troca os valores de duas variáveis sem usar variáveis temporárias.
    - Exemplo: `let a = 5; let b = 10; [a, b] = [b, a]; // Agora 'a' armazena 10 e 'b' armazena 5`

## Estrutura de Repetição

### while (enquanto)

estrutura:

`while (condição) {`

`comandos`

`}`

```JavaScript
let num;
while (num != 0) {
            num = prompt("Digite um número para testar se é par ou ímpar");
            if (num % 2 === 0) {
                alert("O número " + num + " é par");
            }
            else {
                alert("O número " + num + " é ímpar")
            }

        }
```

### do while (repita até)

estrutura:

`do {`

`comandos`

`} while(condição);`

exemplo de código:

```JavaScript
let data = 2024;
        let nome;
        let idade;
        let resultado;
        var decisao;

        do {
            nome = prompt("Qual seu nome?")
            idade = prompt(nome + ", digite sua idade para mostrarmos o ano que você nasceu")
            resultado = data - idade
            alert(nome + ", o ano que você nasceu é " + resultado)
            decisao = prompt("Deseja continuar? [s/n]")
            //caso o usúario digite 's' ele vai repetir o loop, senão ele para o loop
        } while (decisao == "s")
        alert("Procedimento Encerrado")
```