
## O que é Styled-components?

**Styled-components** é uma biblioteca que permite criar estilos no formato de componentes em JavaScript ou TypeScript. No Next, o **styled-components** é uma solução popular para gerenciar estilos, pois suporta server-side rendering (SSR) e permite escrever CSS diretamente dentro de componentes React.

---

## Como configurar Styled-components no Next.js com TypeScript

1. **Instale as dependências necessárias:**
   ```bash
   npm install styled-components @types/styled-components babel-plugin-styled-components
   ```

2. **Configure o Babel:**
   Crie ou edite o arquivo `babel.config.js` para incluir o plugin do styled-components:
   ```javascript
   module.exports = {
     presets: ['next/babel'],
     plugins: [['styled-components', { ssr: true }]],
   };
   ```

3. **Configuração de Tipos:**
   Crie ou edite o arquivo `styled.d.ts` na raiz do projeto para garantir a compatibilidade com o TypeScript:
   ```typescript
   import 'styled-components';

   declare module 'styled-components' {
     export interface DefaultTheme {
       colors: {
         primary: string;
         secondary: string;
       };
     }
   }
   ```

4. **Criando um Tema Global:**
   Defina o tema no seu projeto:
   ```typescript
   // theme.ts
   export const theme = {
     colors: {
       primary: '#0070f3',
       secondary: '#1c1c1c',
     },
   };
   ```

5. **Utilizando o ThemeProvider:**
   Envolva sua aplicação com o `ThemeProvider`:
   ```tsx
   // pages/_app.tsx
   import { ThemeProvider } from 'styled-components';
   import { AppProps } from 'next/app';
   import { theme } from '../theme';

   export default function App({ Component, pageProps }: AppProps) {
     return (
       <ThemeProvider theme={theme}>
         <Component {...pageProps} />
       </ThemeProvider>
     );
   }
   ```

---

## Criando Estilos Globais

O **styled-components** também permite a definição de estilos globais com o `createGlobalStyle`.

1. **Definindo estilos globais:**
   ```typescript
   // styles/global.ts
   import { createGlobalStyle } from 'styled-components';

   export const GlobalStyle = createGlobalStyle`
     *,
     *::before,
     *::after {
       box-sizing: border-box;
       margin: 0;
       padding: 0;
     }

     body {
       font-family: 'Arial', sans-serif;
       background-color: ${({ theme }) => theme.colors.secondary};
       color: ${({ theme }) => theme.colors.primary};
     }
   `;
   ```

2. **Usando os estilos globais:**
   Importe e aplique os estilos globais no arquivo `_app.tsx`:
   ```tsx
   // pages/_app.tsx
   import { ThemeProvider } from 'styled-components';
   import { AppProps } from 'next/app';
   import { theme } from '../theme';
   import { GlobalStyle } from '../styles/global';

   export default function App({ Component, pageProps }: AppProps) {
     return (
       <ThemeProvider theme={theme}>
         <GlobalStyle />
         <Component {...pageProps} />
       </ThemeProvider>
     );
   }
   ```

---

## Exemplo Prático: Criando um Botão Estilizado

```tsx
// components/Button.tsx
import styled from 'styled-components';

interface ButtonProps {
  primary?: boolean;
}

export const Button = styled.button<ButtonProps>`
  background-color: ${({ primary, theme }) =>
    primary ? theme.colors.primary : theme.colors.secondary};
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;

  &:hover {
    opacity: 0.8;
  }
`;
```

**Uso:**
```tsx
// pages/index.tsx
import { Button } from '../components/Button';

export default function Home() {
  return (
    <div>
      <Button primary>Botão Primário</Button>
      <Button>Botão Secundário</Button>
    </div>
  );
}
```

---

## Melhores Práticas

1. **Organize seus Estilos:**
   Mantenha os estilos globais, temas e componentes estilizados em pastas separadas para facilitar a manutenção.

2. **Utilize o Tema:**
   Sempre que possível, utilize o tema para cores e tamanhos para garantir consistência visual.

3. **Estilos Dinâmicos:**
   Aproveite a flexibilidade dos estilos dinâmicos baseados em propriedades, mas mantenha-os simples.

4. **Modularize:**
   Crie componentes reutilizáveis, evitando duplicação de código de estilo.

5. **Testes:**
   Considere usar ferramentas como `jest-styled-components` para garantir que os estilos não sejam alterados inesperadamente.
