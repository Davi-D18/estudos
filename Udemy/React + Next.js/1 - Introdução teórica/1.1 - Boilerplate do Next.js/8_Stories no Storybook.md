## O que são Stories no Storybook?

No contexto do Storybook, um **story** é uma unidade que descreve uma versão de um componente da interface do usuário em um estado específico. Cada story é como um caso de teste visual que documenta como o componente deve ser renderizado sob diferentes condições.

Um story não é apenas uma visualização; ele é um ponto de entrada para explorar, testar e documentar o comportamento e a aparência de um componente isolado do resto do sistema.

### Benefícios dos Stories

1. **Isolamento**: Permitem testar e visualizar componentes fora do contexto da aplicação.
    
2. **Documentação Viva**: Servem como documentação interativa para designers e desenvolvedores.
    
3. **Testes Rápidos**: Ajudam a validar diferentes estados de um componente, acelerando a identificação de problemas.
    
4. **Reutilização**: Os stories servem como base para testes automatizados, validações visuais e exemplos práticos para outros desenvolvedores.
    

---

## Como Criar e Utilizar Stories

### Estrutura Básica de um Story

Um story é basicamente uma função que retorna um componente configurado com props ou estilos específicos. O Storybook então usa essa função para renderizar o componente na interface.

#### Exemplo Básico

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

export default {
  title: 'Example/Button',
  component: Button,
};

export const Default = () => <Button label="Default" onClick={() => console.log('Clicked!')} />;
export const Disabled = () => <Button label="Disabled" disabled />;
export const Primary = () => <Button label="Primary" style={{ backgroundColor: 'blue', color: 'white' }} />;
```

> **Dica:** Cada story exportado deve representar um caso único e importante do componente, cobrindo variações principais de uso.

### Estrutura do Arquivo Stories

1. **Título (**`**title**`**)**: Define a categoria do componente na interface do Storybook. Por exemplo, `Atoms/Button` agrupa o componente na seção `Atoms`.
    
2. **Componente (**`**component**`**)**: Define o componente principal que será testado.
    
3. **Stories Exportadas**: Cada função exportada representa um estado específico do componente.
    

> **Dica:** Use nomes descritivos para os stories, como `Default`, `Hovered`, `WithIcon`, etc. Isso facilita a navegação no Storybook.

### Como Rodar o Storybook

1. Certifique-se de ter instalado o Storybook no projeto:
    
    ```bash
    npx sb init
    ```
    
2. Inicie o Storybook:
    
    ```bash
    npm run storybook
    ```
    
3. Acesse a interface do Storybook em http://localhost:6006.
    

---

## Usando Args para Configurar Stories

Os `args` permitem configurar os props de um componente diretamente na interface gráfica do Storybook, tornando os stories mais dinâmicos.

### Exemplo com Args

```tsx
import React from 'react';
import { Button } from './Button';

export default {
  title: 'Example/Button',
  component: Button,
  argTypes: {
    label: { control: 'text' },
    backgroundColor: { control: 'color' },
  },
};

const Template = (args) => <Button {...args} />;

export const Default = Template.bind({});
Default.args = {
  label: 'Default',
  backgroundColor: 'gray',
};

export const Primary = Template.bind({});
Primary.args = {
  label: 'Primary',
  backgroundColor: 'blue',
};
```

### Personalização com `argTypes`

Os `argTypes` permitem controlar e personalizar os inputs de props na interface do Storybook. Por exemplo:

- **Texto (**`**text**`**)**: Para strings.
    
- **Cores (**`**color**`**)**: Escolha de cores via seletor.
    
- **Booleanos (**`**boolean**`**)**: Para ativar ou desativar funcionalidades.
    

> **Dica:** Use o painel de controles para explorar as variações de props sem alterar o código manualmente.

---

## Melhores Práticas ao Criar Stories

1. **Organização dos Arquivos**:
    
    - Use uma hierarquia clara para agrupar stories. Exemplo: `Atoms/Button`, `Molecules/Card`.
        
2. **Simplicidade**:
    
    - Cada story deve focar em um estado ou cenário único do componente.
        
3. **Uso de Templates**:
    
    - Utilize templates para evitar duplicação de código entre stories.
        
4. **Documentação**:
    
    - Adicione descrições claras para cada story, facilitando a compreensão do contexto.
        
5. **Testes de Acessibilidade**:
    
    - Certifique-se de que os componentes exibidos nos stories sejam acessíveis, usando o addon `a11y`.
        
6. **Histórias Interativas**:
    
    - Use o `controls` para permitir que os usuários manipulem props dinamicamente.
        
7. **Evite Overengineering**:
    
    - Concentre-se nos estados mais importantes do componente e evite criar stories redundantes.
        

---

## Addons Relevantes para Stories

### 1. **Controls**

Permite alterar os props do componente diretamente na interface gráfica do Storybook.

### 2. **A11y**

Valida acessibilidade dos componentes apresentados.

### 3. **Viewport**

Simula diferentes tamanhos de tela para testar a responsividade do componente.

### 4. **Backgrounds**

Configura diferentes cores de fundo para verificar o comportamento visual do componente.

### 5. **Actions**

Monitora eventos disparados pelos componentes, como cliques ou mudanças de estado.

> **Dica:** Instale addons relevantes para o seu projeto usando o comando:

```bash
npm install @storybook/addon-[addon_name]
```

---

## Testando Stories

Os stories também podem ser usados para realizar testes visuais e interativos:

### Testes Visuais com Addons

- Utilize o **Storyshots** para capturar snapshots visuais dos stories e detectar alterações inesperadas na interface.
    

### Testes Interativos

- Integre ferramentas como **Cypress** ou **Testing Library** para validar o comportamento dos componentes nos stories.
    

### Testes com Storybook Test Runner

Storybook agora suporta testes automatizados diretamente na interface. Para configurar:

```bash
npx storybook@latest test
```

---

## Resumo

Os stories são a base do Storybook, permitindo criar documentações vivas, testar estados de componentes de forma isolada e melhorar a comunicação entre times de desenvolvimento e design. Seguir boas práticas ao criar stories resulta em uma biblioteca de componentes mais robusta, reutilizável e acessível. A simplicidade e as ferramentas integradas tornam o Storybook ideal para projetos de qualquer escala.