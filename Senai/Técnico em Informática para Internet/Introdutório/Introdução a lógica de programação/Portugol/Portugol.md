---
Tipo: Aula
Materiais:
  - https://github.com/Davi-D18/Senai
Revisado: Revisando
Inicio: 2024-06-05
Matéria: Lógica de Programação
Última edição: Data inválida
---
> PDF: [https://drive.google.com/file/d/17oK2J6NJ5Ixljzdn5xHG8A40K94j4mqD/view?usp=sharing](https://drive.google.com/file/d/17oK2J6NJ5Ixljzdn5xHG8A40K94j4mqD/view?usp=sharing)

**Portugol** é uma linguagem com regras definidas com uma estrutura formal também conhecido como português estruturado

- As palavras em azul são palavras reservadas, não podem ser usadas na escrita, a não ser que coloque entre aspas
- Usar frases curtas, ser objetivo e simples
- Pensar que nem todo mundo sabe sobre programação, então tornar simples. **Dados de entrada** → **Processamento** → **Saída**

Exemplo:

![[image-1715040639439.jpg6495990198219172138.jpg]]

==Variável: Tipo de Dado==

Funciona dessa maneira aas variáveis no Portugol

Exemplo:

Nome: caractere

Casa, ano: inteiro

![[1000140549.heic]]

## Comandos de Decisão SE SENAO

![[7b55a4c5-3253-4c53-bae4-b67d1ddebf35.png]]

## Exemplo

![[Untitled 2.png|Untitled 2.png]]

  

- Estrutura básica do SE e SENAO
    
    ![[Untitled 1.png]]
    
      
    

## Estrutura de Repetição

![[Untitled 2 2.png|Untitled 2 2.png]]

- Repetição: _==Para==_
    
    ![[Untitled 3.png]]
    
    ![[Untitled 4.png]]
    
    ![[Untitled 5.png]]
    
- Repetição: _==Enquanto==_
    
    ![[Untitled 6.png]]
    
    Enquanto: repetirá aplicando um teste lógico no inicio antes de iniciar a repetição
    
    Pode ser utilizado para fazer um teste lógico de ínicio e ir para a sequência de comandos conforme escrito
    
- Repetição: ==Repita ate==
    
    ![[Untitled 7.png]]
    
    O **repita ate,** teoricamente é mais fácil, ele é a mesma coisa do Enquanto, só que o Repita faz um teste lógico no final do loop
    
    Exemplo: Na imagem acima, o algoritmo perguntará se o usúario deseja confirmar a compra, caso ele escreva “s” (sim) o algoritmo não repetirá o loop, isso porque o teste lógico é `decisao = “s”`, ele vai repetir o loop até o usúario digitar “s”
    
    Se em vez de “s” fosse “n” (não) ele ia repetir o loop mesmo o usúario confirmando a compra
    

**Incremento**: Adicionar

**Decremento**: Subtrair

## Escolha Caso

![[Untitled 8.png]]

Exemplo de Caso Escolha

![[Untitled 9.png]]

  

## Vetores

Vetores posibilitam armazenar mais de um valor em uma única variável

exemplo: `notas: vetor [1..4] de real`

`x, i: inteiro notas: vetor[1..4] de inteiro`

==`Inicio`== `para i de 1 ate 4 faca escreval("Digite um número ") leia(x) notas[i]:= x` ==`fimpara`==

`i:= 1` ==`enquanto`== `(i < 5)` ==`faca`== `escreva(notas[i]) i:= i + 1` ==`fimenquanto`==

O algoritmo pedirá para o usúario digitar 4 números e em seguida vai armazenar no vetor `notas` e imprimir esses valores

- Para imprimir um valor de uma posição do vetor, use o:
    
    - escreva / escreval
    - nome do vetor entre parênteses
    - e em seguida informe a posição do vetor que queira imprimir usando [ ]
    
    Exemplo:
    
    ==`**Var**`==
    
    `notas: vetor[1..4] de inteiro`
    
    ==`**Inicio**`==
    
    ==`**escreva**`==`(notas[1])`
    
    Esse escreva vai imprimir o valor que está no vetor notas na posição 1, caso use um loop ele vai mudar esse número a cada volta `(notas[i])` e vai imprimir os outros valores armazenados em diferentes posições
    
- Ordenando vetores
    
    ![[Untitled 10.png]]
    
    uma estrutura de exemplo para ordenar vetores
    
    Na prática, para ordenar vetores, você precisa comparar o valor que está armazenado na posição 1 do vetor com as outras posições
    
    Na imagem acima mostra como seria essa comparação. Em seguida precisa tirar o valor que estpa naquela posição e armazenar em uma váriavel auxiliar e depois colocar no vetor novamente
    

  

## Matrizes

Estrutura Básica de uma Matriz

Uma estrutura de dados que contém várias váriaveis do mesmo tipo

![[Untitled 11.png]]

Matrizes são compostas de linhas e colunas, como mostrado na imagem acima

Exemplo

![[Untitled 12.png]]