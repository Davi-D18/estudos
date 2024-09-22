![[Pasted image 20240907174849.png]]

## Tipos de Testes
### Testes Unitários
![[Pasted image 20240907175332.png]]
### Testes de Integração
![[Pasted image 20240907175450.png]]
### Testes E2E
![[Pasted image 20240907175654.png]]
![[Pasted image 20240907180218.png]]


![[Pasted image 20240907180500.png]]

Exemplo de teste
```ts
// Todo arquivo de teste, deve conter a extensão .test seguido da extensão do arquivo, tipo JSX / TSX ou JS

function operacaoSoma (num1: number, num2:number) {
	return num1 + num2;
}

test("Aqui é o nome do teste", () => { // Em seguida vem uma função
	const numOne = 10
	const numTwo = 10

	const soma = operacaoSoma(numOne, numTwo);

	expect(soma).toBe(20) // Retorna: teste realizado com sucesso
	// expect vem de espera-se 
		// .toBe vem de igual, tem vários outros por exemplo para ver se
		//retorna um valor booleano
});
```

## Estrutura de Testes
- Renderiação do Componente
- Interações
- Verificar Resultado esperado

Um exemplo de teste de componente:
![[Pasted image 20240908100044.png]]
A primeira importação é importante fazer pois precisa renderizar o componente e verificar se tem algo lá
- `screen`: Algo que está dentro desse componente
- `getByText`: Procura por um texto especifíco
- `toBeInTheDocument()`:  espera-se que aquele texto esteja no documento
- `getByRole()`: Procura um elemento, primeiro parâmetro passa uma role, em seguida passe um objeto e acesse os atributos desse objeto e veja qual quer usar
```ts
screen.getByRole('heading', { level: 1 }) // procure no cabeçalho uma tag h com valor 1
```
- `toHaveTextContent()`:  verifica se um elemento tem um conteúdo em texto, dentro dos parênteses, coloque o texto que quer que ele procure

### Libs
- *userEvent*: Uma biblioteca que simula ações do usuário


![[Pasted image 20240908102848.png]]É bom utiizar um `describe()` para agrupar todo os testes semelhantes por boas práticas