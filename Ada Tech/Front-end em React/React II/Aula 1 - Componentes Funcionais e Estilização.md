
> [Refatoração] Title
> Refatoração vem de atualizar um código antigo ou tornar ele mais legível

# Utilizando props nos componentes funcionais
Nos componentes funcionais, pode utilizar a forma antiga de escrever funções ou utilizar *Arrow Functions* 
```jsx
import React from "react";
function App (props) {
	return (
		<div>
			<h1>{props.tittle}</h1>
		</div>
	)
}
```
O props vai ser um objeto no componente funcional, onde pode acessar utilizando o props e o nome da props
## Desestruturando um objeto
```jsx
import React from "react";
function App ({ tittle, provider, description }) {
	return (
		<div>
			<h1>{tittle}</h1>
		</div>
	)
}

```
Muitas pessoas usam essa forma de desestruturar o objeto para não precisar *props* antes do nome 

> [Criando projeto com TS]
> Criando um projeto React com Typescript (template)
> ao Utilizar o comando clássico para criar um projeto react, adicione isso: 
> npx create-react-app nome-projeto --template typescript```

## Adicionando Tipagem
```tsx
import React from "react";
export const Header: React.FC = () => {
	return (
		<div>
			<h1>Header</h1>
		</div>
	)
}
```
- `React.FC`: Vem de componente no react

## CSS Modules
Basta criar um arquivo CSS normal e em seguida colocar `.modules.css` 
Caso esteja usando usando TypeScript, faça isso: 
```tsx
import React from "react";
import styles from "caminho/para/o/arquivo.module.css"

export const Header: React.FC = () => {
	return (
		<div className={styles.header} >
			<h1>Header</h1>
		</div>

```
TS não recomhece a extensão .modules.css, para resolver, armazene o css em uma variável e em seguida quando for usar as Classes no HTMl, coloque JS e acesse a Class como um objeto "`styles.header`" por exemplo
### Utilizando SASS
O react não entende SASS, precisa baixar uma biblioteca do SASS utilizando o `npm install sass` e colocar a extensão do arquivo de `.modules.scss`

- `:first-child`: Aplica os estilos no primeiro elemento
- `:last-child`: Aplica os estilos no último elemento

## Utilizando interfaces no TS
![[Pasted image 20240820105211.png]]
Utilizando o <> é generic e passar a interface das propriedades 
Ao utilizar isso no TS, quando for importar os componentes ele vai avisar um erro de que precisa passar esses valores que foi definido na interface