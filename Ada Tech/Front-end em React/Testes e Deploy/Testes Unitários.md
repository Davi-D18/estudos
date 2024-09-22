## 1. Principais Comandos do Jest

### 1.1. Estrutura e Organização

Exemplo de teste:

ts

Copiar código

`function operacaoSoma(num1: number, num2: number) {   return num1 + num2; }  test("Deve retornar a soma correta", () => {   const numOne = 10;   const numTwo = 20;    const soma = operacaoSoma(numOne, numTwo);    expect(soma).toBe(30); });`

- `describe()`: Agrupa testes relacionados. Serve para organizar os testes em blocos lógicos.
- `test()` ou `it()`: Define um caso de teste. Ambos são equivalentes.
- `beforeEach()` / `afterEach()`: Executa uma função antes ou depois de cada teste.
- `beforeAll()` / `afterAll()`: Executa uma função antes ou depois de todos os testes no bloco.

### 1.2. Verificações (Matchers)

Exemplo de uso de `expect` com `toBe`:

ts

Copiar código

`expect(1 + 2).toBe(3);`

- `expect()`: Inicia uma asserção, geralmente seguido por um matcher.
- `toBe()`: Compara valores primitivos (uso de `===`).
- `toEqual()`: Compara valores de objetos ou arrays.
- `toBeTruthy()` / `toBeFalsy()`: Verifica se um valor é verdadeiro ou falso.
- `toHaveBeenCalled()`: Verifica se uma função foi chamada.
- `toHaveBeenCalledWith()`: Verifica se uma função foi chamada com parâmetros específicos.
- `toThrow()`: Verifica se uma função lança uma exceção.

### 1.3. Mocks e Spies

Exemplo de `jest.fn()`:

ts

Copiar código

`const funcaoMock = jest.fn();`

- `jest.fn()`: Cria uma função mock (falsa) que pode ser monitorada.
- `jest.spyOn()`: Cria um espião para uma função existente.
- `mockImplementation()`: Define a implementação de uma função mock.
- `mockResolvedValue()` / `mockRejectedValue()`: Define valores de resolução/rejeição para mocks de Promises.

## 2. React Testing Library (RTL)

### 2.1. Renderização e Acesso

Exemplo de renderização de componente:

```ts
render(<MeuComponente />);
```


- `render()`: Renderiza um componente React para teste.
- `screen.getByText()`: Seleciona um elemento baseado no texto visível.
- `screen.getByRole()`: Seleciona um elemento baseado na sua role (função/propósito).
- `screen.queryByText()`: Similar ao `getByText`, mas retorna `null` se o elemento não for encontrado (não lança erro).
- `screen.findByText()`: Retorna uma Promise que resolve quando o elemento é encontrado (usado para testes assíncronos).

### 2.2. Eventos

Exemplo de `fireEvent`:

ts

Copiar código

`fireEvent.click(screen.getByText('Clique Aqui'));`

- `fireEvent()`: Dispara eventos (clique, mudança, etc.) em elementos.
- `userEvent`: Biblioteca recomendada para simular interações de usuários (substitui `fireEvent`).

## 3. Principais Roles com `getByRole`

### 3.1. Botões e Controles

Exemplo de `getByRole` para selecionar um botão:

ts

Copiar código

`const botao = screen.getByRole('button', { name: /enviar/i });`

- `button`: Usado para selecionar botões.
- `textbox`: Usado para selecionar campos de entrada de texto (`<input>` com `type="text"` ou `<textarea>`).
- `checkbox`: Usado para selecionar checkboxes.

### 3.2. Estrutura e Navegação

Exemplo de `getByRole` para selecionar um cabeçalho:

ts

Copiar código

`const heading = screen.getByRole('heading', { level: 1 });`

- `heading`: Seleciona elementos de cabeçalho (`<h1>`, `<h2>`, etc.).
- `link`: Usado para selecionar links (`<a>`).
- `navigation`: Seleciona a barra de navegação (`<nav>`).

### 3.3. Feedback e Status

Exemplo de `getByRole` para selecionar um alerta:

ts

Copiar código

`const alerta = screen.getByRole('alert');`

- `alert`: Seleciona alertas ou mensagens de erro.
- `status`: Seleciona elementos que indicam status atual (como carregamento).

### 3.4. Media e Conteúdo

Exemplo de `getByRole` para selecionar uma imagem:

ts

Copiar código

`const imagem = screen.getByRole('img', { name: /logo/i });`

- `img`: Usado para selecionar imagens (`<img>`).
- `article`: Seleciona elementos de artigo (`<article>`).

## 4. Dicas Importantes

- Sempre preferir `getByRole`: Garante que você está testando o que o usuário final realmente vê e interage.
- Utilize Queries com Sabedoria: `getBy*` lança erro se o elemento não é encontrado, `queryBy*` retorna `null`, e `findBy*` lida com operações assíncronas.
- Teste o Comportamento, Não a Implementação: Concentre-se no que o usuário experimenta, em vez de detalhes de implementação específicos.

---

# Anotações de Estudo: Testes Unitários com Jest e React Testing Library (Continuação)

## 5. Testes Unitários de Componentes

### 5.1. Renderização de Componentes

Exemplo de teste de renderização simples:

ts

Copiar código

`test('deve renderizar o componente', () => {   render(<MeuComponente />);   expect(screen.getByText('Texto do Componente')).toBeInTheDocument(); });`

- Teste de Renderização Simples: Verifique se o componente renderiza corretamente sem erros.
- Verificação de Props: Teste se o componente exibe as informações corretas com base nas props.

### 5.2. Interações e Eventos

Exemplo de teste de clique em botão:

ts

Copiar código

`test('deve chamar a função ao clicar no botão', () => {   const handleClick = jest.fn();   render(<MeuComponente onClick={handleClick} />);   userEvent.click(screen.getByRole('button'));   expect(handleClick).toHaveBeenCalledTimes(1); });`

- Clique em Botões: Teste o comportamento de um botão ao ser clicado.
- Mudanças em Inputs: Verifique como o componente responde a mudanças em campos de entrada.

### 5.3. Testando Estados e Efeitos

Exemplo de teste de comportamento condicional:

ts

Copiar código

`test('deve exibir conteúdo condicionalmente', () => {   render(<MeuComponente mostrar={true} />);   expect(screen.getByText('Conteúdo Visível')).toBeInTheDocument(); });`

- Testando Comportamento Condicional: Verifique como o componente se comporta com diferentes estados internos.
- Hooks Customizados: Se o componente usa hooks customizados, você pode testar o comportamento com diferentes estados.

## 6. Testes Unitários de Funções

### 6.1. Testando Funções Puras

Exemplo de teste de função pura:

ts

Copiar código

`function soma(a: number, b: number) {   return a + b; }  test('deve retornar a soma correta', () => {   expect(soma(2, 3)).toBe(5); });`

- Funções Puras: São funções que retornam o mesmo resultado para os mesmos argumentos e não causam efeitos colaterais.

### 6.2. Testando Funções Assíncronas

Exemplo de teste de Promise:

ts

Copiar código

`async function fetchData() {   return 'dados'; }  test('deve retornar os dados', async () => {   const dados = await fetchData();   expect(dados).toBe('dados'); });`

- Testando Promises: Para funções que retornam Promises, use `async/await` ou os métodos `.resolves` / `.rejects`.
- Simulando Rejeições: Teste o comportamento quando a Promise é rejeitada.

### 6.3. Testando Funções com Efeitos Colaterais

Exemplo de teste de função com dependência externa:

ts

Copiar código

`function salvarDados(api, dados) {   return api.salvar(dados); }  test('deve chamar API com os dados corretos', () => {   const apiMock = { salvar: jest.fn() };   salvarDados(apiMock, { nome: 'Luiz' });   expect(apiMock.salvar).toHaveBeenCalledWith({ nome: 'Luiz' }); });`

- Funções com Dependências Externas: Use mocks para simular comportamentos de dependências externas.

## 7. Outras Técnicas e Conceitos Importantes

### 7.1. Teste de Snapshots

Exemplo de teste de snapshot:

ts

Copiar código

`test('deve corresponder ao snapshot', () => {   const { container } = render(<MeuComponente />);   expect(container).toMatchSnapshot(); });`

- Snapshot Testing: Captura o "snapshot" (foto instantânea) da saída de um componente e compara com execuções futuras.

### 7.2. Cobertura de Testes

Exemplo de comando para gerar cobertura de código:

bash

Copiar código

`jest --coverage`

- Cobertura de Código: Use a flag `--coverage` com o Jest para gerar relatórios de cobertura de testes.

### 7.3. Testando Componentes com Contexto

Exemplo de teste de componente com Context API:

ts

Copiar código

`test('deve acessar o valor do contexto', () => {   render(     <MeuContexto.Provider value={valor}>       <MeuComponente />     </MeuContexto.Provider>   );   expect(screen.getByText('Valor do Contexto')).toBeInTheDocument(); });`

- Context API: Para testar componentes que usam Context API, você pode envolver o componente com o provedor de contexto no teste.

### 7.4. Testando Componentes Conectados ao Redux

Exemplo de teste com Redux:

ts

Copiar código

`import { Provider } from 'react-redux'; import { createStore } from 'redux';  test('deve acessar o estado do Redux', () => {   const store = createStore(reducer);   render(     <Provider store={store}>       <MeuComponente />     </Provider>   );   expect(screen.getByText('Valor do Redux')).toBeInTheDocument(); });`

- Testes com Redux: Para componentes conectados ao Redux, você pode usar o `Provider` do Redux para fornecer a store ao componente.

### 7.5. Mocking de Módulos e Funções Globais

Exemplo de mocking de módulo:

ts

Copiar código

`jest.mock('axios', () => ({   get: jest.fn().mockResolvedValue({ data: 'dados' }), }));`

- Mocking de Módulos: Simule módulos inteiros para isolar o que está sendo testado.

Exemplo de mocking de funções globais:

ts

Copiar código

`jest.spyOn(global.Math, 'random').mockReturnValue(0.5);`

- Mocking de Funções Globais: Simule funções globais, como `Date` ou `Math.random`.

## 8. Conclusão e Melhores Práticas

- Isolar Testes: Sempre isole o que está sendo testado para garantir que o teste se concentra em um único comportamento.
- Escreva Testes Confiáveis: Um bom teste deve ser previsível, repetível, e não deve quebrar sem uma mudança real no código.
- Refatore os Testes: Como qualquer código, testes também devem ser claros e mantidos em boas condições.