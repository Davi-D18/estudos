Link documentação: https://storybook.js.org/recipes/next#next
## O que é o Storybook?

O **Storybook** é uma ferramenta de desenvolvimento usada para criar, visualizar e testar componentes de UI (Interface do Usuário) de forma isolada. Ele ajuda a construir e documentar componentes de forma independente, sem a necessidade de integrá-los à aplicação principal durante o processo de desenvolvimento.

### Principais Benefícios

1. **Desenvolvimento Isolado**: Permite criar e testar componentes individualmente, sem dependências externas.
    
2. **Documentação Automática**: Gera uma biblioteca interativa que serve como documentação viva.
    
3. **Testes Visuais**: Detecta mudanças inesperadas na UI (com snapshots visuais).
    
4. **Design Systems**: Facilita a criação e o gerenciamento de bibliotecas de design reutilizáveis.
    

---

## Como Usar o Storybook

### 1. Instalação

Antes de instalar o Storybook, é necessário ter um projeto configurado com **React**, **Vue**, **Angular** ou qualquer outra biblioteca suportada.

```bash
# Instale o Storybook no seu projeto:
npx storybook@latest init
# Para projetos com next, use o comando acima
```

Este comando configura o Storybook para o seu projeto, criando os arquivos de configuração necessários.

---

### 2. Criando um "Story"

Um **story** é uma representação de um estado de um componente. Ele descreve como o componente deve ser renderizado em um determinado contexto.

**Exemplo para um botão no React:**

**Componente: Button.jsx**

```tsx
import React from 'react';
import './button.css';

export const Button = ({ label, onClick }) => (
  <button className="btn" onClick={onClick}>
    {label}
  </button>
);
```

**Story: Button.stories.jsx**

```tsx
import React from 'react';
import { Button } from './Button';

// Título no Storybook e categoria
export default {
  title: 'Example/Button',
  component: Button,
};

// Exemplo de diferentes estados do botão
export const Primary = () => <Button label="Primary" />;
export const Disabled = () => <Button label="Disabled" onClick={() => {}} disabled />;
export const WithClick = () => <Button label="Click Me!" onClick={() => alert('Button clicked!')} />;
```

> **Comentário**: O arquivo `.stories.jsx` define como cada estado do componente será visualizado no Storybook.

---

### 3. Executando o Storybook

Após criar seus stories, execute:

```
npm run storybook
```

Isso iniciará o Storybook em um servidor local, geralmente disponível em `http://localhost:6006`.

---

## Funcionalidades do Storybook

### 1. **Docs**

Geração automática de documentação baseada nos seus componentes e seus props.

### 2. **Addons**

Extensões para funcionalidades extras, como acessibilidade, testes visuais e mais.

### 3. **Controle de Props**

Permite alterar dinamicamente as propriedades de um componente pela interface gráfica do Storybook.

#### Exemplo de Controle de Props

```tsx
export const ConfigurableButton = (args) => <Button {...args} />;
ConfigurableButton.args = {
  label: 'Dynamic Button',
  onClick: () => alert('Dynamic click!'),
};
```

---

## Melhores Práticas

1. **Organize Stories**: Categorize bem os componentes e mantenha uma hierarquia clara, como `Atoms`, `Molecules` e `Organisms`.
    
2. **Adote Addons**:
    
    - Use o **Addon Controls** para manipular props em tempo real.
        
    - Adicione **Snapshots Visuais** para testes de regressão.
        
3. **Foco em Acessibilidade**: Utilize o addon **a11y** para verificar problemas de acessibilidade.
    
4. **Documentação Reutilizável**: Centralize a documentação para toda a equipe (designers, desenvolvedores e PMs).
    
5. **Teste Interativo**: Configure testes interativos com ferramentas como Cypress ou Testing Library.
    

---

## Resumo

O Storybook é uma ferramenta essencial para desenvolvedores modernos, facilitando o desenvolvimento isolado, documentando componentes automaticamente e melhorando a comunicação com equipes de design e produto. Ele acelera o fluxo de trabalho, garante consistência e reduz problemas relacionados à interface.