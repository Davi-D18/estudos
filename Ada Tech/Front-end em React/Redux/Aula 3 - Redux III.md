# Refatorando um código Redux da versão antiga para versão nova

Basta instalar a versão recente do Redux 
```bash
 yarn add @reduxjs/toolkit 
 ```
Em seguida no arquivo `store.ts` basta refatorar o código antigo para essa forma:
![[Pasted image 20240907112845.png]]
Ao usar o `configureStore()` ele recebe um objeto, dentro do objeto tem um parâmetro que é obrigatório, o *reducer* é nele onde vai ser colocado o root que engloba todos os reducers

No *middleware* coloca um array e coloca o logger que é aquela biblioteca que mostra tudo que tá acontecendo no Redux

## Refatorando
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

export const userSlice = createSlice({
initialState, // estado inicial
name: "user", // nome do reducer (vai ser usado na hora de fazer os dispatchs)
reducers: { // Aqui é onde fica cada método desse reducer
	// primeira action
	login: (state, action) => { 
		state.user = action.payload;
	},
	// segunda action
	logout: (state, action) => {
		state.user = null;
	},
},

});

export const { login, logout } = userSlice.actions; 
// não é obrigatório essa exportação dessa forma, mas facilota para usar em outros componentes
```


