Link da documentação: [Hook de Efeito](https://react.dev/reference/react/useEffect)

# O que é Hook de Efeito(useEffect)?
Ele permite que você execute efeitos colaterais em componentes funcionais. **Efeitos colaterais** são ações que ocorrem em resposta a mudanças no componente, como buscar dados de uma API, configurar subscriptions, ou manipular o DOM diretamente.

## Equivalência 
Esse hook é equivalente aos métodos de componentes em classes:
- `componentDidMount`
- `componentDidUpdate`
- `componentwillUnmount`
[[Aula 4 - Ciclo de Vida]]

## Utilizando o useEffect 
```tsx
useEffect(funcaoDisparada, dependencies)
```
`funcaoDisparada` é a função que será disparada
`dependencies` será as variáveis que o React ficará monitorando, caso elas mudem ele chamará a função que foi colocada
```tsx

useEffect(() => {
	console.log("Executando a função useEffect...")
}, []) // esse array vazio é onde estará as dependencias
```
Quando o array está vazio, significa que ele executará apenas uma vez o useEffect que é quando o componente for montado 

### Cleanup Function 
Caso no useEffect você coloque um `return`, você poderá acessar o método do ciclo de vida `componentWillUnmount` em outras palavras, será executado essa função quando o componente for desmontado da tela
```tsx

useEffect(() => {
	console.log("Executando a função useEffect...")
	
	return () => {
		console.log("Será executado essa função ao desmontar o componente")
	}
}, [toggle]);
```

# Salvando informações com localStorage e pegando essas Informações
![[Pasted image 20240823144424.png]]
**Imagine que você tem um formulário:**

- Você preenche o formulário e clica em "Salvar".
- O React, usando o `useState`, atualiza a tela para mostrar as novas informações.
- **Mas:** Se você tentar salvar essas informações no `localStorage` imediatamente, elas podem não ser salvas corretamente.

**Por que isso acontece?**

- **Renderização:** Quando o React atualiza a tela, ele precisa refazer todo o processo de renderização.
- **Tempo:** Durante essa renderização, o código que salva no `localStorage` pode ser executado antes que a nova informação seja completamente atualizada no estado do componente.

**A Solução: Um Pequeno Atraso Estratégico**

- **Novo array/função:** Em vez de salvar diretamente no `localStorage`, você cria um novo array ou uma nova função para armazenar as informações temporariamente.
- **useState:** Só depois de ter certeza que as informações estão corretas e completas, você usa o `useState` para atualizar o estado do componente com esse novo array ou função.
- **localStorage:** Com o estado atualizado, você pode salvar as informações no `localStorage` com segurança.

**Por que isso funciona?**

- **Garantia de atualização:** Ao usar um intermediário (novo array/função), você garante que a informação a ser salva está sempre atualizada.
- **Evita problemas de tempo:** Ao salvar após a atualização do estado, você evita que o `localStorage` seja atualizado com dados incompletos.

![[Pasted image 20240823145516.png]]Ao utilizar o `useEffect` com array vazio (dependencia) ele executará ao recarregar a página ou montar o componente, vai no `localStorage` e pega a informação e converte ela para um array (pois quando está no `localStorage` está em formato de string) e seta ela para o estado `setTasks`