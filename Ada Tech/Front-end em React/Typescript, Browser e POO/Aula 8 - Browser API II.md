# Adicionando eventos em Javascript
Existe vários tipos de eventos, é bom consultar a documentação da MDN.
Um exemplo simples de como funciona os eventos em Javascript
```js
const button = document.querySelector('button');
button.addEventListener('click', (event) => {
	alert('Botão clicado')
});
```

Estrutura básica de um evento
```js
Element.addEventListener('nome-do-evento', (parâmetro) => {
	// função que será disparada quando ocorrer o evento
})
```

## Um exemplo
![[Pasted image 20240806104601.png]]
No exemplo acima, é um contador que contém botões para aumentar e diminuir o valor

## Adicionando estilos ou removendo
É possível adicionar classes em elementos por meio do JS
### Inline
```js
const contadorElemento = document.querySelector('#contador');
contadorElemento.style.color = "red";
// váriavel que contem o elemento html + .style + propriedade css = valor
```

### Adicionando ou removendo classes
```js
contadorElemento.classList.add("btn"); // adiciona uma classe
contadorElemento.classList.remove("btn"); // remove uma classe
```

## Web Storage API 
![[Pasted image 20240806111353.png]]

> [Importante]
> Ambos os métodos abaixo, utilizam o conceito chave-valor, parecido com um object

![[Pasted image 20240806111615.png]]

#### localStorage
![[Pasted image 20240807203845.png]]

- `setItem`: Adiciona uma chave com valor
- `getItem`: Passe uma chave como parâmetro e ele retorna o valor da chave
- `removeItem`: Você passa uma chave e ele remove tanto a chave como o valor
- `clear`: Não tem parâmetros, limpa todos os dados

No `sessionStorage`, os propcedimentos são os mesmos, *com a diferença que esses dados serão perdidos ao fechar a aba do navegador*, ao contrario do `localStorage` que armazena localmente e essa informação não é perdida

> [getItem] Recuperando uma informação no localStorage
> O retorno do método `getItem` sempre será em formato de string
> Contents

### Um exemplo
![[Pasted image 20240807210304.png]]
![[Pasted image 20240807211401.png]]

Para evitar repetir código, pode adicionar essa alteração de tema em uma function

Print acima guarda uma informação do tema da página
- `window.unload()` : Ao carregar a página, fará algo que estiver dentro da função
- O ternário na função onload não é necessário, escrevendo menos código

- O código vai acessar o localStorage e procurar a chave referente ao tema na função `onload`
- Em seguida, adiciona um evento ao botão que quando clicado recebe um valor true ou false na váriavel darkTheme
- Salva essa informação novamente no localStorage e aplica os estilos caso seja verdadeiro, caso seja falso, mantém o tema claro