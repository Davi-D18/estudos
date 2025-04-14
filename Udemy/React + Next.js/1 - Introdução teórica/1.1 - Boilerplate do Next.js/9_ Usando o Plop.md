Link: https://plopjs.com/documentation/#getting-started
## O que é o Plop.js?

O **Plop.js** é uma ferramenta de scaffolding que automatiza a criação de arquivos e códigos de maneira consistente em projetos. Ele é altamente configurável e usa templates e geradores para criar componentes, arquivos de configuração, serviços, entre outros.

### Por que usar o Plop.js?

- **Consistência**: Garante que arquivos e códigos sigam padrões predefinidos.
    
- **Automação**: Reduz tarefas repetitivas, como criar estruturas de pastas e arquivos.
    
- **Flexibilidade**: Pode ser configurado para diferentes tipos de projetos, como front-end, back-end ou bibliotecas.
    

---

## Como Funciona o Plop.js?

1. **Plopfile**: Um arquivo de configuração (`plopfile.js`) define os geradores.
    
2. **Geradores**: São funções que criam arquivos com base em templates e interações do usuário.
    
3. **Templates**: Arquivos modelo que servem como base para o conteúdo gerado.
    

---

## Como Configurar o Plop.js (Versão 4)

### 1. Instalar o Plop

Execute o comando abaixo para instalar o Plop como dependência de desenvolvimento:

```
npm install --save-dev plop
```

> **Dica:** Você também pode instalar globalmente para acessar o Plop em qualquer projeto:

```
npm install -g plop
```

### 2. Criar o Arquivo de Configuração

No diretório raiz do seu projeto, crie o arquivo `plopfile.js`. Este arquivo define os geradores e templates.

**Exemplo de plopfile.js básico:**

```js
module.exports = function (plop) {
  // Defina um gerador chamado "component"
  plop.setGenerator('component', {
    description: 'Cria um novo componente',
    prompts: [
      {
        type: 'input',
        name: 'name',
        message: 'Qual o nome do componente?'
      }
    ],
    actions: [
      {
        type: 'add',
        path: 'src/components/{{pascalCase name}}/{{pascalCase name}}.jsx',
        templateFile: 'plop-templates/component.hbs'
      },
      {
        type: 'add',
        path: 'src/components/{{pascalCase name}}/{{pascalCase name}}.css',
        templateFile: 'plop-templates/component.css.hbs'
      }
    ]
  });
};
```

### 3. Criar Templates

Os templates são arquivos que definem o conteúdo dos arquivos gerados. Use variáveis para substituir valores dinamicamente. Todos os templates devem conter a extensão `.hbs` no final

**Exemplo de** `**component.hbs**`

```jsx
import React from 'react';
import './{{pascalCase name}}.css';

export const {{pascalCase name}} = () => {
  return (
    <div className="{{kebabCase name}}">
      <h1>{{pascalCase name}} Component</h1>
    </div>
  );
};
```

**Exemplo de** `**component.css.hbs**`

```
.{{kebabCase name}} {
  display: flex;
  align-items: center;
  justify-content: center;
}
```

### 4. Rodar o Plop

Para executar o Plop, use o comando:

```
npx plop
```

Escolha o gerador e siga as instruções interativas.

---

## Funcionalidades Avançadas

### Personalização de Prompts

Os **prompts** permitem interagir com o usuário para obter entradas personalizadas. Tipos comuns:

- `input`: Entrada de texto.
    
- `list`: Lista de opções.
    
- `confirm`: Confirmação (sim/não).
    
- `checkbox`: Seleção múltipla.
    

**Exemplo com múltiplos prompts:**

```js
prompts: [
  {
    type: 'input',
    name: 'name',
    message: 'Qual o nome do componente?'
  },
  {
    type: 'confirm',
    name: 'addStyle',
    message: 'Deseja adicionar um arquivo CSS?'
  }
]
```

### Condições em Ações

Use condições para gerar arquivos apenas quando necessário.

**Exemplo:**

```js
{
  type: 'add',
  path: 'src/components/{{pascalCase name}}/{{pascalCase name}}.css',
  templateFile: 'plop-templates/component.css.hbs',
  skip: (answers) => !answers.addStyle && 'CSS não será criado.'
}
```

### Hooks Customizados

Adicione lógica antes ou depois de uma ação usando `plop.setActionType`.

**Exemplo:**

```js
plop.setActionType('log', (answers, config) => {
  console.log(config.message);
  return 'Log concluído';
});
```

### Helpers para Templates

Os **helpers** permitem criar lógica personalizada nos templates. Exemplos comuns incluem manipulação de strings.

**Adicionar um Helper:**

```js
plop.setHelper('uppercase', (text) => text.toUpperCase());
```

**Usar no Template:**

```js
const COMPONENT_NAME = '{{uppercase name}}';
```

---

## Melhores Práticas

1. **Organização**:
    
    - Mantenha os templates em uma pasta separada (`plop-templates`).
        
2. **Consistência**:
    
    - Use helpers e funções padrão para garantir a uniformidade dos nomes de arquivos e classes.
        
3. **Documentação**:
    
    - Adicione descrições claras nos prompts e nos geradores.
        
4. **Reutilização**:
    
    - Crie geradores modulares para diferentes partes do projeto (ex.: componentes, serviços, hooks).
        
5. **Validação**:
    
    - Valide as entradas dos usuários para evitar erros.
        

**Exemplo de Validação:**

```js
{
  type: 'input',
  name: 'name',
  message: 'Digite um nome válido:',
  validate: (input) => input ? true : 'O nome não pode estar vazio.'
}
```

6. **Automação Completa**:
    
    - Combine Plop.js com scripts npm para automatizar fluxos inteiros.
        

**Exemplo:**

```json
"scripts": {
  "generate:component": "plop --generator component"
}
```

---

## Ferramentas Complementares

1. **Hygen**:
    
    - Similar ao Plop, mas com foco em comandos rápidos via CLI.
        
2. **Yeoman**:
    
    - Ferramenta robusta para scaffolding com mais funcionalidades, mas menos simples que o Plop.
        
3. **CLI Personalizado**:
    
    - Combine o Plop com ferramentas como `Commander.js` para criar sua própria CLI.
        

---

## Resumo

O Plop.js é uma ferramenta poderosa para scaffolding, ideal para garantir consistência e produtividade em projetos de qualquer escala. Com sua simplicidade e flexibilidade, é uma escolha popular entre desenvolvedores que buscam automatizar tarefas repetitivas e criar fluxos de trabalho personalizados.