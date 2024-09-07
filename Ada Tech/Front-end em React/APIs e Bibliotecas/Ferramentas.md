*[Styled Components](https://styled-components.com)*: Basicamente aplica CSS junto com JavaScript #styled-components
	==Importante:== Ao utilizar essa biblioteca junto com TS, precisa instalar outra biblioteca de tipagem para o TS, no caso essa: `@types/styled-components` só pesquisar la no NPM ou instalar via linha de comando (se não tiver mudado a forma de instalar) 

*[Redux](redux.js.org)* : Resolve aquele problema do React de compartilhar vários estados e variáveis em diferentes componentes, Amplamente utilizado 
	É bom utilizar a lib *react-redux* para integrar melhor ambos
	*redux-logger* : Tudo que acontece no redux, essa lib mostra no terminal
	
[Jest](https://jestjs.io): Biblioteca de testes unitários
*React testing library*: Uma biblioteca de testes únitários mais focada em React

Tanto o Jest como o React testing library, já vem instalados no projeto react ao usar o `yarn create react-app`

Exemplo de teste unitário com Jest:
![[Pasted image 20240907182311.png]]
Nesse caso o teste é realizzado com sucesso
25