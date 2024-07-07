Regra CSS `line-height:` Espaçamento entre linhas

- `block`: ocupa o bloco todo
- `inline`: vai ficar dentro da própria linha
- `flex`: normalmente coloca o flex dentro de um elemento pai que contenha os elementos que queremos mudar as posições
- `justify-content`: alinha os elementos na posção que você colocar

## Flexbox

- `display: flex;`: Transforma o elemento em um contêiner flexível e permite o uso das propriedades flex.
- `flex-direction: row | row-reverse | column | column-reverse;`: Define a direção dos elementos flex.
- `flex-wrap: nowrap | wrap | wrap-reverse;`: Define se os itens devem quebrar a linha ou não.
- `justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;`: Alinha os elementos ao longo do eixo principal.
- `align-items: stretch | flex-start | flex-end | center | baseline;`: Alinha os elementos no eixo transversal.
- `align-content: stretch | flex-start | flex-end | center | space-between | space-around;`: Alinha as linhas de flex no eixo transversal quando há espaço extra.

## Grid Layout

- `display: grid;`: Transforma o elemento em um contêiner de grade e permite o uso das propriedades de grade.
- `grid-template-columns: <track-size> ... | <line-name> ...;`: Define o tamanho e o nome das linhas de grade na direção de coluna.
- `grid-template-rows: <track-size> ... | <line-name> ...;`: Define o tamanho e o nome das linhas de grade na direção de linha.
- `grid-column-start: <line>;` e `grid-column-end: <line>;`: Define onde um item de grade começa e termina na direção da coluna.
- `grid-row-start: <line>;` e `grid-row-end: <line>;`: Define onde um item de grade começa e termina na direção da linha.

## Flexbox Simplificado

- `display: flex;`: Torna o elemento um contêiner flexível.
- `flex-direction:`: Define a direção dos elementos, seja em linha ou em coluna.
- `flex-wrap:`: Determina se os itens devem quebrar a linha ou não.
- `justify-content:`: Alinha os elementos horizontalmente.
- `align-items:`: Alinha os elementos verticalmente.
- `align-content:`: Alinha as linhas de flex quando há espaço extra.

## Grid Layout Simplificado

- `display: grid;`: Torna o elemento um contêiner de grade.
- `grid-template-columns:`: Define o tamanho e o nome das colunas da grade.
- `grid-template-rows:`: Define o tamanho e o nome das linhas da grade.
- `grid-column-start:` e `grid-column-end:`: Define onde um item de grade começa e termina horizontalmente.
- `grid-row-start:` e `grid-row-end:`: Define onde um item de grade começa e termina verticalmente.

## Grid Layout com `repeat()`

- `repeat()`: Esta função é usada para repetir um padrão de tamanho e linha de grade múltiplas vezes. Ela simplifica a definição do tamanho das colunas ou linhas.

Por exemplo, se quisermos criar uma grade com 4 colunas de mesmo tamanho, em vez de escrever `grid-template-columns: 1fr 1fr 1fr 1fr;`, podemos simplificar e escrever `grid-template-columns: repeat(4, 1fr);`.

```css
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  /* Isso cria 4 colunas de igual largura */
}

```

Além disso, `repeat()` pode ser combinado com outras unidades de medida e funções. Por exemplo, para criar uma grade com duas colunas de 100px e duas colunas que ocupem o espaço restante igualmente, você poderia escrever `grid-template-columns: repeat(2, 100px) repeat(2, 1fr);`.

```css
.container {
  display: grid;
  grid-template-columns: repeat(2, 100px) repeat(2, 1fr);
  /* Isso cria duas colunas de 100px seguidas por duas colunas que ocupam o espaço restante */
}

```

Essa função também pode ser útil para repetir um padrão complexo. Por exemplo, se você quiser repetir um padrão de três colunas onde a primeira tem 100px, a segunda ocupa o espaço restante e a terceira tem 200px, você pode fazer isso com `grid-template-columns: repeat(3, 100px 1fr 200px);`.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 100px 1fr 200px);
  /* Isso cria uma repetição de três colunas: a primeira com 100px, a segunda ocupando o espaço restante e a terceira com 200px */
}

```

A função `repeat()` é uma ferramenta poderosa para tornar o seu CSS mais enxuto e legível, especialmente ao trabalhar com layouts de grade complexos.

Exemplos de como o Grid Layout pode ser usado com comentários explicativos.

```css
/* Exemplo 1: Definindo um contêiner de grade com três colunas de igual largura */
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  /* 1fr significa que cada coluna terá uma fração igual do espaço disponível */
}

/* Exemplo 2: Definindo um contêiner de grade com duas linhas, uma maior que a outra */
.container {
  display: grid;
  grid-template-rows: 2fr 1fr;
  /* 2fr para a primeira linha significa que ela ocupará o dobro do espaço da segunda linha */
}

/* Exemplo 3: Posicionando um item de grade em uma área específica da grade */
.item {
  grid-column-start: 1; /* A contagem das colunas começa em 1 */
  grid-column-end: 3; /* Esta instrução faz o item se esticar desde a primeira até a terceira coluna */
  grid-row-start: 2; /* A contagem das linhas começa em 1 */
  grid-row-end: 4; /* Esta instrução faz o item se esticar desde a segunda até a quarta linha */
}

```

Outros exemplos

```css
/* Exemplo 4: Criando uma grade com áreas nomeadas */
.container {
  display: grid;
  grid-template-areas:
    "header header header"
    "sidebar main main"
    "footer footer footer";
  /* Este código cria uma grade com um cabeçalho, um rodapé e uma área principal com uma barra lateral */
}

/* Exemplo 5: Colocando itens em áreas nomeadas */
.item1 {
  grid-area: header;
  /* Este item será colocado na área 'header' da grade */
}

.item2 {
  grid-area: main;
  /* Este item será colocado na área 'main' da grade */
}

/* Exemplo 6: Criando uma grade com colunas e linhas de diferentes tamanhos */
.container {
  display: grid;
  grid-template-columns: 200px auto 200px;
  grid-template-rows: 50px auto 50px;
  /* Este código cria uma grade com colunas de 200px, uma coluna auto e linhas de 50px */
}

```

Estes exemplos demonstram algumas das capacidades do Grid Layout em CSS. Use-os como referência para criar seus próprios layouts.
