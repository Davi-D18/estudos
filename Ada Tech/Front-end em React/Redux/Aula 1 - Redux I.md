![[Pasted image 20240905103738.png]]

*Reducer* nada mais é do que um armazenamento, onde vai guardar variáveis e estados ou outras coisas relacionais
*Root Reducer* Agrupa todos os outros Reducers 

![[Pasted image 20240905104831.png]]

![[Pasted image 20240905105954.png]]Link: [whimsical](https://whimsical.com/redux-VRMDFyyXby3WaZ3n8uTEGB)

# Utilizando Redux (Forma mais antiga)
Dentro da Biblioteca do Redux, existe um carinha chamado `combineReducers()` onde ele é criado em um arquivo TS / JS e atribui ele a uma variável, dentro desse método irá ter todos os reducers da aplicação(envolva elas em forma de objeto)
```ts
import { combineReducers } from "redux"
import { useReducer } from "diretorio"

export const rootReducer = combineReducer({
	useReducer,
})

```
Esse arquivo de root-reducer, deve ser criado dentro da pasta redux, porém na raiz daquela pasta
![[Pasted image 20240905132046.png]]No componente App, envolva toda a aplicação com um provider
```tsx
import React from "react";
import { Header } from "diretorio";
import { Cart } from "diretorio";

import { store } from "./redux/store";

function App (props) {
	return (
		<Provider store={store}>
			<Header />
			<Cart />
		</Provider>
	)
}
```
Dessa forma, a aplucação toda terá acesso as funcções e variáveis dentro do provider

Ao usar o provider no App, ele vai informar que precisa passar um valor *store* (Basicamente um armazenamento), então basta criar um arquivo `store.ts` ao lado do arquivo root
```ts
import { createStore } from "redux"
import { rootReducer } from "./root-reducer"

export const store = createStore(rootReducer)
```

essa é a cofiguração inicial do redux

Quando tiver usando TS com Redux, ele vai apresentar uns erros de tipagem, por isso é bom colocar uma tipagem para o root, tipo essa:
![[Pasted image 20240905135600.png]]No componente que você for usar algo que está armazenado em um reducer, utilize o `useSelector()` passando uma função e escolhendo qual reducer quer acessar
```tsx
import { useSelector } from "react-redux"

export const Header: React.FC = () => {
	const objeto = useSelector((rootReducer: RootReducer) => rootReducer.userReducer); // Aqui é a tipagem em "RootReducer"
}
```

Ao tratar as informações no Reducer em alguma função, é recomendado fazer dessa forma: 
```ts
interface User {

name: string;

email: string;

}

  

interface UserState {

user: User | null;

}

  

const initialState: UserState = {

user: null,

};

  

interface UserAction {

type: string;

payload?: User;

}
export function userReducer(state = initialState, action: UserAction) {
	if (action.type === "user/login") // é recomendado começar com o nome do reducer, seguido da ação {
		return {
			...state,
			user: action.payload as User,
			// informando que os dados do usuário tem que vim
		}
	}
}
```

## Utilizando o dispatch()

```ts
import { useDispatch } from "redux"
const dispatch = useDispatch()
```

![[Pasted image 20240905142135.png]]
Outra ferramenta útil é o *redux-logger* nessa ferramenta tudo que acontece no redux é mostrado no terminal

### Configurando redux-logger
#### Instalando 
```bash
npm i -D redux-logger
```

#### Configurando
No arquivo `store.ts` pode fazer essas configurações:
```ts
import { applyMiddleware, createStore } from 'redux';

import logger from 'redux-logger'

const store = createStore(

  reducer,

  applyMiddleware(logger) // Essa linha basicamente indica que ele vai interceptar tudo do redux para mostrar no terminal

)
```

