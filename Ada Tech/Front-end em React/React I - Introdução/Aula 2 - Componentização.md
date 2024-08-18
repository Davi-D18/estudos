# Padrões de Renderização
- *SPA (Single Page Application)* : Aplicações de Página Única 
- *SSR (Single Server Rendering)* : 
- *SSG (Single Site Generation)* : 

# Tipos de Componente
### Class Component
Ainda muito utilizado, é a forma antiga
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
*Componente em classe é uma classe que herda a classe component do React, e retorna HTML dentro de um método render*
Também pode ter variáveis nessa classe utilizanddo o constructor e usar no HTML
```jsx
import React from "react";
class App extends React.Component {
	constructor() {
		super() // herda as classes do component react
		this.nome = "Davi"
	}
	render() {
		return (
			<div>
				<h1>Component</h1>
				<h2>{this.nome}</h2> // o retorno será o conteúdo que 
				// está na variável
			</div>
		)
	}
}

```

> [Importante] Atomic Design Methodology
> É uma métodologia de design onde divide grandes aplicações em pequenas partes e vai montando o site 
> Contents

*É importante criar uma pasta com componentes no projeto e lá colocar os componentes e CSS referentes, depois importa no `App.jsx` para renderizar na página*



