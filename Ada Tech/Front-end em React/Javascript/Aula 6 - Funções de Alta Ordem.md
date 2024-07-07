[[Aula 5 - Funções e Objects]]
![[Pasted image 20240629110555.png]]
Um exemplo básico de uma função que retorna outra função como parâmetro

## 2° Exemplo de uma função que recebe outra função como parâmetro
![[Pasted image 20240629111951.png]]
Basicamente, você cria várias funções atribuindo elas a uma variável e cria outra função que vai receber parâmetros junto com o nome de alguma das funções que foi criada e em seguida repassar esses parâmetros para a função escolhida


Também é possível injetar uma operação ou comandos dentro de uma função de alta ordem:
![[Pasted image 20240629113013.png]]


### Funções de Arrays
Algumas funções mais usadas em Arrays
![[Pasted image 20240629113355.png]]

### forEach()
esse método de array vai percorrer um array específico passando uma função como parâmetro
```jsx
const numeros = [40, 50, 60, 80, 25]

function percorrerElementos (elementos) {
	console.log(elementos);
}

numeros.forEach(percorrerElementos);
// aqui vai percorrer os elementos do array numeros 
// em seguida vai chamar uma função

```
outro forma de percorrer o elemento:
```jsx
const numeros = [50, 13, 50, 80, 60]

numeros.forEach((Elementos) => {
	console.log(Elementos)
});

//irá imprimir normalmente, só foi simplificado 
```

```jsx
numeros.forEach((Elementos, index, arrayCompleto) => {
	console.log(Elementos, index, arrayCompleto);
});

//é possivel passar até 3 parâmetros na função forEach()
// elementos é o elemento do array
// index é o indice ou posição daquele elemento no array
// arrayCompleto é o array completo 
```

### find()
verifica se um elemento existe naquele array utilizando uma condição
```jsx
numeros.find((elementos) => {
	return elementos ==== 10
})

const pessoas [
{
nome: "joão"
idade: 25
},
{
nome: "Sabrina"
idade: 26
},
]
//também é possivel fazer um array de objetos
```
outro exemplo:
```jsx
const pessoas [
{
nome: "joão"
idade: 25
},
{
nome: "Sabrina"
idade: 26
},
{
nome: "Marcos"
idade: 30
}
]

const pessoaEncontrada = pessoas.find((idade) => {
	idade > 28
});
```
### findIndex()
é a mesma coisa do find, a diferença que o findIndex vai retornar o índice do elemento no array
```jsx
pessoas.findIndex((elementos) => {
	return elementos ==== 25
})
```
quando o findIndex() não encontra nenhum elemento que satisfaça a condição, ele retorna -1
significando que não foi encontrado





