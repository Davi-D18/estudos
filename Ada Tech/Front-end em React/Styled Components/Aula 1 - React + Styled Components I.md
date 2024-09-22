*CSS in JS*
![[Pasted image 20240901151329.png]]

Um exemplo :
![[Pasted image 20240901153336.png]]
```tsx
const Tittle = styled.h1`
	color: red;
`;
```
Depois de criar um componente com o nome que deseja utilize o `styled` depois coloque a tag que você quer que aquele componente seja ao ser renderizado no React, abra crases e escreva os estilos normalmente
Essa lib, ela usa meio que um SCSS, então pode utilizar a forma do SCSS dentro dos componentes estilizados

## Criando estilos globais com a Lib
Basta criar um arquivo novo com o nome que desejar e clocar no final `.ts / .js` depois importe a lib no arquivo e crie um componente estilizado seguido de `createGlobalStyle`
```tsx
import styled from "styled-components"

export const GlobalStyle = createGlobalStyle`
	margin: 0;
	padding: 0;
	box-sizing: border-box;
`
```

Provavelmente vai ter uma confusão ao usar essa lib por ela ser parecida com um componente funcional, para resolver, basta fazer o seguinte:
```tsx
import * as S from "styled-components"
// Astericos indica que tá importando tudo
// o S é um préfixo, significa que para acessar aquele estilo 

export const Header: React.FC = () => {
	return (
		<S.Tittle> Conteúdo de uma div <S.Tittle>
	)
} 
```
basta usar o S. e o nome do componente para acessar ele

No React também tem uma biblioteca de Icons, se chama `react-icons`
```tsx

import { FiLogIn } from "react-icons/fi" // depois do barra, coloca o provedor dos icons, basta olhar na documentação e as duas priemiras letras é do provedor

<FiLogIn />
```
A maioria dos icons ou todos devem ser SVG, então para estilizar basta colocar um seletor de svg nos styles 