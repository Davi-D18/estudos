
# React Testing Library e Jest

## **1. O que são React Testing Library e Jest?**

### **React Testing Library**
- Biblioteca para testar componentes React com foco no comportamento do usuário.
- Promove boas práticas ao testar a aplicação da forma como o usuário final interagiria.
- Foco na acessibilidade e em encontrar elementos por rótulos, texto visível, etc.

### **Jest**
- Framework de teste completo para JavaScript, incluindo assertions, mocking e snapshots.
- Ótimo suporte para testes de React, com integração fácil ao React Testing Library.

---

## **2. Como configurar?**

### **Passo 1: Instalar dependências**
Execute o seguinte comando no terminal para instalar as dependências principais:

```bash
npm install --save-dev jest @testing-library/react @testing-library/jest-dom @testing-library/user-event
```

Se você estiver usando TypeScript, adicione também:

```bash
npm install --save-dev @types/jest
```

### **Passo 2: Configurar Jest**
1. Crie um arquivo de configuração para Jest, chamado `jest.config.js`:
   ```javascript
   module.exports = {
       testEnvironment: "jsdom",
       setupFilesAfterEnv: ["<rootDir>/jest.setup.js"],
   };
   ```

2. Crie o arquivo `jest.setup.js` para configurar o ambiente:
   ```javascript
   import '@testing-library/jest-dom';
   ```

3. Adicione um script ao `package.json` para rodar os testes:
   ```json
   "scripts": {
       "test": "jest"
   }
   ```

### **Passo 3: Estrutura do Projeto**
Organize os testes no diretório `__tests__` ou siga o padrão de colocar arquivos com `.test.js` ou `.spec.js` ao lado dos componentes.

---

## **3. Princípios básicos para testes**

### **Encontrando elementos**
- Use queries do Testing Library para localizar elementos:
  - `getByText`: Busca elementos pelo texto visível.
  - `getByRole`: Busca elementos acessíveis por seu papel (ex: botão, título).
  - `getByLabelText`: Usa rótulos de formulário associados.

Exemplo prático:
```javascript
import { render, screen } from '@testing-library/react';
import App from './App';

test('renderiza um botão de enviar', () => {
    render(<App />);
    const button = screen.getByRole('button', { name: /enviar/i });
    expect(button).toBeInTheDocument();
});
```

### **Simulando eventos**
- Use a biblioteca `user-event` para simular cliques, digitação e interações.

Exemplo prático:
```javascript
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import App from './App';

test('botão incrementa o contador ao clicar', async () => {
    render(<App />);
    const button = screen.getByRole('button', { name: /incrementar/i });
    await userEvent.click(button);
    expect(screen.getByText(/contador: 1/i)).toBeInTheDocument();
});
```

Explicação:
- **`render(<App />);`**: Renderiza o componente no DOM virtual.
- **`screen.getByRole`**: Localiza o botão pelo seu papel e texto.
- **`await userEvent.click(button);`**: Simula o clique no botão.
- **`expect`**: Verifica se o texto esperado está presente no DOM.

### **Mocking**
- Mock funções ou módulos para isolar comportamentos.

Exemplo prático:
```javascript
jest.mock('./api', () => ({
    fetchData: jest.fn(() => Promise.resolve({ data: 'mockado!' })),
}));

test('usa dados mockados na API', async () => {
    const { fetchData } = require('./api');
    fetchData.mockResolvedValueOnce({ data: 'dados mockados!' });

    expect(fetchData).toHaveBeenCalled();
});
```

---

## **4. Dicas importantes**
- **Teste o comportamento, não a implementação**: Os testes devem refletir a experiência do usuário.
- **Prefira queries acessíveis**: Use `getByRole`, `getByLabelText` sempre que possível.
- **Estruture os testes**:
  1. **Setup**: Renderize o componente ou configure o ambiente.
  2. **Ação**: Simule interações do usuário.
  3. **Asserção**: Verifique os resultados esperados.
- **Use snapshots com cuidado**: Ideais para verificar mudanças visuais em componentes estáveis.
- **Automatize testes**: Configure seu CI/CD para rodar testes automaticamente.

---

## **5. Recursos adicionais**
- Documentação oficial:
  - [React Testing Library](https://testing-library.com/docs/react-testing-library/intro/)
  - [Jest](https://jestjs.io/docs/getting-started)

---

## **6. Checklist rápido**
1. [ ] Instale as dependências.
2. [ ] Configure o ambiente com Jest.
3. [ ] Escreva testes baseados em comportamento.
4. [ ] Execute os testes com `npm test` ou `yarn test`.
5. [ ] Garanta alta cobertura sem sobrecarregar com testes irrelevantes.

