### Every()
every verifica se todos os elementos de um array atendem a uma condição
ele sempre vai retornar um valor booleano (true || false)
```jsx
const numeros = [10, 40, 50, 25, 15, 3]

const numerosPositivos = numeros.every((elementos) => elementos > 15 ) 
console.log(numerosPositivos) // retorna false

````

### Some()
o método some() verifica se pelo menos um dos elementos do array satisfaça uma condição
```jsx
const numeros = [10, 40, 50, 25, 15, 3]
const algumElementoAtendeCondicao = numeros.some((elemento) => elemento > 5)
//retorna true porque pelo menos um dos elementos é maior que 5
```
### map()
retorna um novo array com a mesma quantidade de elementos do array original a cada interação 
```jsx
const numeros = [10, 40, 50, 25, 15, 3]
const arrayNovo = numeros.map((elementos) => {
	return elementos * 2
})
//retorna um novo array mas com cada elemento multiplicado por 2
```
um exemplo:

```jsx
const carrinho = [
	{produto: "Feijão", preco: 7.98, quantidade: 3}
	{produto: "Arroz", preco: 4.98, quantidade: 5}
	{produto: "Leite 1L", preco: 6.99, quantidade: 2}
];

const carrinhoComTotal = carrinho.map((item) => {
	return {
		...item,
		total: item.preco * item.quantidade,
	};
});
// ...item vai pegar todo o array e adicionar no novo array com o preço embaixo
```

### filter()
filter() vai criar um novo array a partir do original, porém vai filtrar os elementos que satisfazer uma determinada condição e adicionar nesse novo array
```jsx
const numeros = [10, 40, 50, 25, 15, 3]

const pares = numeros.filter((numero) => numero % 2 === 0);
console.log(pares);
// vai retornar os números que satisfazer a condição que foi imposta
// [10, 40, 50]
```

### reduce() 
essa função vai pegar os elementos de um array e reduzir elas a um único número, pelo menos é esse o princípio, dá para fazer mais coisas, porém o foco é esse, ao final da função, deve colocar o valor incial onde o acumulador irá iniciar depois do fechamento das { } seguido por uma vírgula 
no reduce(), são 4 parâmetros: `acumulador, elemento, index, arrayCompleto`
- `acumulador`: o resultado 
- `elemento`: cada elemento do array
- `index`: índice
- `arrayCompleto`: array como um todo
```jsx
const numeros = [1, 2, 3, 4, 5]

const numerosReduzidos = numeros.reduce((acumulador, elementos) => {
	return elementos + acumulador
}, 0);
```
caso queria ignorar um dos parâmetros, use o __ para ignorar
```jsx
const carrinho = [
	{produto: "Feijão", preco: 7.98, quantidade: 3}
	{produto: "Arroz", preco: 4.98, quantidade: 5}
	{produto: "Leite 1L", preco: 6.99, quantidade: 2}
];

const totalAPagar = carrinho.reduce((total, item) => {
	return item.preco * item.quantidade + total
}, 0);

console.log(totalAPagar);
// retornará o total da compra
