![[Pasted image 20240908142123.png]]

Pode criar um arquivo `setupTest.js` e colocar a importação do `testing-library/jest-dom` que vai funcionar em todos os testes normalmente

É possível pegar uma tag também pelo id, pode colocar um atributo em um componente estilizado chamaado `data` em seguida coloque - e o nome que quer colocar
```tsx
<S.Headercontainer data-testeid="total"> Teste </S.Headercontainer>
```
Facilita para pegar algo no JS ou TS
e pode pegar essa informação no arquivo de testes 
```tsx

const totalElement = screen.getByTestId("total"); 
```


- `toBeEmptyDOMElement()`: Verifica se uma tag está com conteúdo vazio

Outro exemplo:
![[Pasted image 20240909140547.png]]

40