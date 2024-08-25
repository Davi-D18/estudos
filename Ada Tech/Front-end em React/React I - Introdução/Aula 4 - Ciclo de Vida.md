![[Pasted image 20240819094507.png]]
# Fases do Ciclo
- Montagem
- Atualização
- Desmontagem

## Montagem
![[Pasted image 20240819095112.png]]
## Atualização
![[Pasted image 20240819095750.png]]
## Desmontagem
![[Pasted image 20240819095857.png]]

# Métodos do Ciclo de Vida
#CicloDeVida
## Montagem 
- `Constructor()`
- `componentWillMount`
- `componentDidMount`
- `render`

Esses métodos funcionam como funções de seta ( arrow functions )
O método `componentWillMount` não é mais recomendado utilizar por ser inseguro, caso queira usar, adicione um `UNSAFE_` antes do método 

Um exemplo:
![[Pasted image 20240819102954.png]]

```jsx
{ this.state.showCounter ? <Counter /> : null }
```


> [StrictMode] Title
> O `StrictMode` é bastante importante para achar erros na aplicação, ele renderiza os componentes duas vezes para pegar algum tipo de bug
> `Re-render` é o processo de renderizar novamente o componente


## Atualização
![[Pasted image 20240819105317.png]]

## Desmontagem
![[Pasted image 20240819145423.png]]

### Removendo eventos ao usar o componentWillUnmount()
![[Pasted image 20240819150314.png]]