![[Pasted image 20240902104558.png]]

Exemplo usando:
![[Pasted image 20240902111740.png]]

O ideal seria criar os contexto dentro de uma pasta chamada *context* e criar um componente com o nome que preferir seguido de *Context.jsx / tsx*

Para criar um contexto, use o `createContext()` e para acessar uma variável / função do *provider* use o `useContext()`

*Provider*: Provider é o componente onde estão as variáveis / funções 

Detalhe: No component `App` envolva os componentes utilizando a variável que recebe o `createContext` para esses componentes acessarem as variáveis / funções, exemplo:
```tsx
import { TasksContent } from "../diretorio/do/provider";
export const App: React.FC = () => {
	return (
		<TasksContent>
			<Header />
			<Tasks />
		</TasksContent>
	)
};
```

![[Pasted image 20240902113719.png]]

Interfaces e importações ficam fora da função (que é o componente em si) já as variáveis que queremos compoartilhar, funções, arrays e etc, ficam dentro do componente, na imagem acima demonstra isso

## Importando no componente
![[Pasted image 20240902114354.png]]
Para acessar essas funções / variáveis, no componente que você quer importar, importe o arquivo e declare um array onde você vai pegar só o que precisa e atribua para um `useContext()` colocando entre parênteses a variável que tá sendo exportada lá no arquivo

### Utilizando estilos com condicional
```jsx

<input 
	className{task.done ? style.done : '' }
/> 
```
No exemplo acima tá utilizando SCSS por isso tá em forma de objeto
