# Tipos de Importação e Exportação
Em vez de fazer a importação e exportação de componentes da forma padrão
```jsx

import React from "react";
class App extends React.Component {
	// A classe App herda do component react
	// em seguida usa o método render para renderizar
	render() {
		return (
			<div>
				<h1>Component</h1>
			</div>
		)
	}
}

export default App;
```
Pode optar por uma forma "melhor" e que te força a colocar o nome exato do componente
```jsx
import React from "react";
export class App extends React.Component {
	// A classe App herda do component react
	// em seguida usa o método render para renderizar
	render() {
		return (
			<div>
				<h1>Component</h1>
			</div>
		)
	}
}

```
Importando 
```jsx
import { App } from "./diretorio/do/componente"
```
*Essa forma acaba sendo melhor pelo fato de não poder renomear o componente, facilitando na hora de compreender*

## Retornando mais de um componente 
No React, não permite renderizar mais de um componente sem estar dentro de uma tag, exemplo:
```jsx
import React from "react";
export class App extends React.Component {
	// A classe App herda do component react
	// em seguida usa o método render para renderizar
	render() {
		return (
			<Navbar />
			
			<Article />
			// não é permitido isso
		)
	}
}
```
Porém para resolver, pode fazer isso:
```jsx
import React from "react";
export class App extends React.Component {
	// A classe App herda do component react
	// em seguida usa o método render para renderizar
	render() {
		return (
			<>
				<Navbar />
			
				<Article />
			</>
		)
	}
}
```
Esse `<>` seria um fragment do React criado para esses casos
# Reutilizando Componentes
Basicamente, os componentes são nada mais que tags especiais, sendo assim, pode colocar atributos dentro do componente que está sendo importado no App.jsx 
```jsx

import React from "react";
export class App extends React.Component {
	// A classe App herda do component react
	// em seguida usa o método render para renderizar
	render() {
		return (
			<>
				<Navbar />
				
				<article className="articles">
					<Article tittle="Exemplo de Título"/>
					<Article />
					<Article />
					<Article />
				</article />
			</>
		)
	}
}
```
Agora lá no componente que está recebendo esses atributos, você pode fazer assim:
```jsx
import React from "react";
export class App extends React.Component {
	// A classe App herda do component react
	// em seguida usa o método render para renderizar
	render() {
		return (
			<div>
				<h1>{this.props.tittle}</h1>
				// Isso vem de POO, está acessando as props (ppropriedades)
				// E está pegando o atributo tittle e está implementando
				// No componente
			</div>
		)
	}
}
```
## Estilizando componentes inline
Para fazer isso, basta apenas usar os estilos inline na tag html porém em formato de objeto:
```jsx
import React from "react";
export class App extends React.Component {
	// A classe App herda do component react
	// em seguida usa o método render para renderizar
	render() {
		return (
			<div style{{ marginTop: "20px", padding: "5px" }}>
				<h1>{this.props.tittle}</h1>
				// Isso vem de POO, está acessando as props (ppropriedades)
				// E está pegando o atributo tittle e está implementando
				// No componente
			</div>
		)
	}

```

# Estados
![[Pasted image 20240818100705.png]]
Para usar um estado, vá no constructor do component e crie um estado que é um objeto que vai receber 1 ou mais estados e atribua um valor
Em seguida, vai no elemento que deseja adicionar um estado e adiciona um evento e dentro do evento ele vai mudar um estado do componente como na imagem acima

Outro exemplo:
![[Pasted image 20240818101712.png]]