# Hooks
Hooks são nada mais que métodos de acessar o ciclo de vida dos componentes sem escrever classes em componentes funcionais 
## Identificando um Hook
Todos os Hooks no React sempre começam com a palavrinha `use` 

## Hook de Estado
```tsx
import React from "react";
export const Header: React.FC = () => {
	const [valorInicial, funcaoParaAlterarOEstado] = useEstate(0) // o 0 seria o valor inicial, pode ser tambem ''
	return (
		<div>
			<h1>Header</h1>
		</div>
	)
}
```
Gelera utiliza uma abordagem de boas práticas que ma função que vai alterar o estado, usa-se esse padrão:
```tsx
import React, { useState } from "react"

export const Header: React.FC = () => {
	const [contador, setContador] = usestate(0)
	return {
		<h2> {contador} </h2>	
		
		<button onClick{() => {
			setContador( contador + 1 )
		}}> Aumentar</button>
	}
}
```

### Um exemplo
![[Pasted image 20240821105656.png]]

![[Pasted image 20240821111804.png]]
![[Pasted image 20240821112838.png]]Gerando um id diferente: 
```tsx
id: new Date().getTime()
```

