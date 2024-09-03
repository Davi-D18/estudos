# O que é o `useMemo`?

O `useMemo` é um Hook do React que serve para **memorizar** o resultado de um cálculo caro, ou seja, uma função que leva tempo para ser executada. Ao memorizar o resultado, o React evita reexecutar essa função a cada renderização, a menos que as dependências da função mudem. Isso otimiza o desempenho da sua aplicação, especialmente em componentes complexos que realizam muitos cálculos.

**Quando usar o `useMemo`?**

- **Cálculos complexos:** Funções que envolvem muitos loops, operações matemáticas intensivas ou acesso a dados externos.
- **Resultados que não mudam com frequência:** Se o resultado de uma função raramente se altera, não há necessidade de recalculá-lo a cada renderização.
- **Componentes com muitas re-renderizações:** Em componentes que são renderizados com frequência, o `useMemo` pode evitar recalcular valores que não mudaram, melhorando o desempenho.

**Como usar o `useMemo`?**

JavaScript

```jsx
import { useMemo } from 'react';

function MyComponent({ data }) {
  const calculatedValue = useMemo(() => {
    // Cálculo complexo aqui
    return expensiveCalculation(data);
  }, [data]);

  // ...
}
```

- **Primeiro argumento:** A função que realiza o cálculo.
- **Segundo argumento:** Um array de dependências. A função será recalculada apenas se algum valor nesse array mudar.

**Exemplo prático:**

JavaScript

```jsx
function ExpensiveList({ items }) {
  const filteredItems = useMemo(() => {
    return items.filter(item => item.price > 100);
  }, [items]);

  return (
    <ul>
      {filteredItems.map(item => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```

Neste exemplo, o `useMemo` é usado para filtrar uma lista de itens. A lista filtrada será recalculada apenas quando o array `items` mudar.

**Considerações importantes:**

- **Dependências:** Escolha as dependências com cuidado. Adicionar mais dependências do que o necessário pode levar a recalculações desnecessárias.
- **Overuse:** Evite usar o `useMemo` em excesso. Memorizar todos os valores pode levar a um aumento no consumo de memória.
- **Outros Hooks:** O `useMemo` pode ser combinado com outros Hooks como o `useCallback` para otimizar ainda mais o desempenho.

![[Pasted image 20240901095800.png]]
Um exemplo: ![[Pasted image 20240901101759.png]]
## Utilizando o useMemo
![[Pasted image 20240901104550.png]]

# useCallback
![[Pasted image 20240901143449.png]]
## Uso do useCallback

```tsx

const aplicarDesconto = useCallback((desconto: number) => {
	return totalOutcomes * (1 - desconto)
}, [totalOutcomes])

```
Esse hook de memoização guarda apenas a *definição da variável*, não guarda a função como um todo. E é interessante utilizar em cálculos complexos que exigem da máquina, porém a galera quase não utiliza