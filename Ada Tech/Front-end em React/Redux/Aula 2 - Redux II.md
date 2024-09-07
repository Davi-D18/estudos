```ts
export function cartProducts(state = initialState, action: CartAction) {

switch (action.type) {

	case "cart/add-product":
		return {
		...state,
		
		cart: [...state.cart, action.payload],
		
	};

	case "cart/remove-product":
	
		const productASerRemovido = action.payload;
		
		const cartFiltered = state.cart.filter(
		
		(product) => product.id !== productASerRemovido.id
		
		);
		
		return {
		
		...state,
		
		cart: cartFiltered,
		
		};
	
	default:
	
		return state;

	}

}
```

A função `cartReducer()` vai basicamente remover ou adicionar um produto do carrinho