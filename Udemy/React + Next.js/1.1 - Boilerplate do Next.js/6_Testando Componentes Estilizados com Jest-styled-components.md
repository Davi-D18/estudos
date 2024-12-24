
## O que é Jest-styled-components?

**Jest-styled-components** é uma extensão para o Jest que facilita testar estilos de componentes desenvolvidos com **styled-components**. Ele permite verificar estilos CSS dinamicamente e comparar snapshots estilizados.

## Como usar?

1. **Instalação**:
   ```bash
   npm install --save-dev jest-styled-components
   ```

2. **Configuração**:
   Certifique-se de importar no início do arquivo:
   ```javascript
   import 'jest-styled-components';
   ```

3. **Testando Estilos**:
   Use ferramentas como **React Testing Library** ou **Enzyme** para renderizar o componente.

## Desafios Práticos

### Desafio 1: Testando estilos com `toHaveStyleRule`
Crie um botão estilizado e verifique sua cor de fundo.

#### Código do Componente:
```javascript
// Button.js
import styled from 'styled-components';

export const Button = styled.button`
  background-color: ${(props) => (props.primary ? 'blue' : 'gray')};
  color: white;
  padding: 10px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
`;
```

#### Testes:
```javascript
import React from 'react';
import { render } from '@testing-library/react';
import { Button } from './Button';
import 'jest-styled-components';

test('o botão primário tem fundo azul', () => {
  const { container } = render(<Button primary />);
  expect(container.firstChild).toHaveStyleRule('background-color', 'blue');
});

test('o botão secundário tem fundo cinza', () => {
  const { container } = render(<Button />);
  expect(container.firstChild).toHaveStyleRule('background-color', 'gray');
});
```

#### Saída esperada:
```plaintext
PASS  Button.test.js
✓ o botão primário tem fundo azul
✓ o botão secundário tem fundo cinza
```

---

### Desafio 2: Usando Snapshot para Estilos
Certifique-se de que a aparência do botão estilizado não mudou ao longo do tempo.

#### Teste com Snapshot:
```javascript
test('snapshot do botão primário', () => {
  const { container } = render(<Button primary />);
  expect(container.firstChild).toMatchSnapshot();
});
```

---

## Melhores Práticas

1. **Escreva Testes Significativos:**  
   Teste apenas estilos críticos e dinâmicos, não estilos óbvios.

2. **Snapshot com Moderação:**  
   Use snapshots para componentes com estilos complexos, mas prefira testes específicos.

3. **Evite Lógica Excessiva nos Estilos:**  
   Garanta que os estilos sejam simples e fáceis de prever.

4. **Combine com Outras Ferramentas:**  
   Utilize **React Testing Library** para interações e estados visuais além dos estilos.
