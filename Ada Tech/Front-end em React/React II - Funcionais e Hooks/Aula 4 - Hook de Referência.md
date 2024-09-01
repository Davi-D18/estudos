Um hook de referência é uma ferramenta que nos permite criar referências mutáveis a valores. Isso significa que podemos armazenar um valor e modificá-lo diretamente, sem precisar re-renderizar o componente toda vez que o valor mudar.

**Para que serve?**

- **Acessar elementos DOM:** Permite selecionar elementos do DOM e manipulá-los diretamente.
- **Manter valores entre renderizações:** Armazena valores que não precisam ser re-renderizados a cada atualização do componente, como contadores ou valores de formulários.
- **Criar efeitos colaterais:** Pode ser usado em conjunto com o `useEffect` para executar efeitos colaterais que não dependem do estado do componente.

**Como funciona o `useRef`?**

O hook mais comum para criar referências é o `useRef`. Ele retorna um objeto com uma propriedade `.current` que pode armazenar qualquer valor.

JavaScript

```jsx
import { useRef } from 'react';

function MeuComponente() {
  const inputRef = useRef(null);

  const handleClick = () => {
    inputRef.current.focus();
    // current é a "chave" para acesar o valor que é um objeto
  };

  return (
    <div>
      <input ref={inputRef} />
      <button onClick={handleClick}>Focar   1. blog.shravaniroy.com blog.shravaniroy.com no input</button>
    </div>
  );
}
```

**No exemplo acima:**

- `inputRef` é uma referência ao elemento de input.
- Ao clicar no botão, o método `handleClick` foca no input usando `inputRef.current.focus()`.

**Quando usar `useRef`?**

- **Acessar elementos DOM:** Para focar em um elemento, medir suas dimensões ou realizar outras operações diretamente no DOM.
- **Manter valores entre renderizações:** Para armazenar valores que não precisam ser re-renderizados, como IDs de elementos ou contadores.
- **Criar efeitos colaterais:** Em conjunto com o `useEffect`, para executar efeitos colaterais que não dependem do estado do componente, como iniciar animações ou configurar listeners de eventos.

**Outros hooks de referência:**

- **`useImperativeHandle`:** Permite expor uma API personalizada para um componente filho.
- **`forwardRef`:** Permite criar componentes que podem receber uma referência como prop.

**Pontos importantes:**

- **Não re-renderiza:** O valor de `.current` não dispara uma nova renderização do componente.
- **Mutável:** O valor de `.current` pode ser modificado diretamente.
- **Inicialização:** O valor inicial de `.current` é passado como argumento para `useRef`.

**Em resumo:**

Os hooks de referência são ferramentas poderosas que nos permitem manipular o DOM e manter valores entre renderizações. Ao entender como eles funcionam, você poderá criar componentes mais complexos e interativos em React.

![[Pasted image 20240831184638.png]]

Apesar que ao usar o `useRef` e não renderizar diretamente o componente, pode ser útil em alguns cenários, como:

- Pegar elementos html da página:
```jsx
function MeuComponente() {
	const inputRef = useRef(null);

	useEffect(() => {
		console.log(inputRef)
		// Já que um ref não dispara uma re-renderização no react, pode usar
		// um useEffect para pegar esse valor
	}, [inputRef])
  return (
    <div>
      <input ref={inputRef} />
      // no React, cada elemento HTMl possui esse atributo "ref"
    </div>
  );
}
```

![[Pasted image 20240901092438.png]]Exemplo utilizando formulários:
![[Pasted image 20240901093734.png]]