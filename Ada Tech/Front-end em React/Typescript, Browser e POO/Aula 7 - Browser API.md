# DOM API
![[Screenshot_20240804_182216_Brave.jpg]]
![[Screenshot_20240804_182424_Brave.jpg]]
É possível escutar muito por aí a seguinte frase "a árvore de elementos do DOM"

## Utilizando o document
![[Pasted image 20240709095758.png]]
```js
// 1° método 
const todosP = document.getElementsByTagName('p')
console.log(todosP);

// 2° Método 
const todosContainer = document.getElementsByClassName('container')
console.log(todosContainer);

// 3° Método (Mais indicado para formulários com names) 
const todosName = document.getElementsByName('email')
console.log(todosName);

// 4° Método
const id = document.getElementsById('principal')
console.log(id)

// 5° Método (mais utilizado)
const seletor = document.querySelector('div > ul > li')
// esse método funciona como um seletor do CSS, a mesma forma de usar lá pode se usar aqui no Javascript
console.log(seletor);
// outra forma de pegar várias tags de uma vez 
const seletor = document.querySelectorAll('p')
//vai pegar todos os elementos p
```


### Alterando elementos com document
- `textContent`: Seleciona um conteúdo de uma tag
	- exemplo: `primeiroParagrafo = primeiroParagrafo.textContent`
	- Vai pegar todo o conteúdo da tag ignorando tags dentro dessa tag, como `strong`
- `innerHTML`: Seleciona o conteúdo de uma tag porém mostra as tags que estão dentro
	- exemplo: `primeiroParagrafo = primeiroParagrafo.innerHTML
- `value`:  vai pegar o value de um input

```js
primeiroParagrafo.innerHTML = "Outro conteúdo"
//isso vale para o textContent
```


### Inserindo mudanças no HTML
##### 1° Forma 
![[Pasted image 20240805113153.png]]
o `.appendChild` tem a ideia de adicionar ao final de uma tag

##### 2° Forma

```js
const listaUl = document.querySelector('ul')
const listaLi = document.querySelectorAll('ul > li')
listaUl.insertBefore(novaTagli, listaLi[1]);
// insertBefore: no primeiro arugumento adiciona a tag e no segundo a posição
```


### Removendo conteúdos
o `removeChild` deve ser usado no pai que está contendo os filhos
```js
listaUl.removeChild(novaTagLi)
//novaTagLi uma variável
```

