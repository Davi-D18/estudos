Link: https://docs.github.com/pt/actions
## O que é o GitHub Actions?

O **GitHub Actions** é uma plataforma de integração contínua (CI) e entrega contínua (CD) integrada ao GitHub. Ele permite criar fluxos de trabalho automatizados para compilar, testar e implantar seu código diretamente a partir do repositório GitHub.

### Principais Funcionalidades:

- **Integração Contínua (CI)**: Automatize o teste e a compilação de código a cada mudança.
    
- **Entrega Contínua (CD)**: Implante aplicações automaticamente em ambientes de produção ou testes.
    
- **Automação Personalizada**: Crie workflows para tarefas personalizadas, como linting, geração de relatórios ou notificações.
    
- **Acesso a Marketplace**: Reutilize ações pré-criadas da comunidade.
    

---

## Como Funciona o GitHub Actions?

### Conceitos Fundamentais:

1. **Workflow**:
    
    - Um arquivo YAML que define uma sequência de etapas para automação.
        
    - Localizado na pasta `.github/workflows` do repositório.
        
2. **Jobs**:
    
    - Um conjunto de etapas que são executadas em paralelo ou sequencialmente.
        
3. **Steps**:
    
    - Tarefas individuais dentro de um job.
        
    - Podem executar scripts ou usar ações predefinidas.
        
4. **Actions**:
    
    - Blocos reutilizáveis para tarefas comuns, como configurar um ambiente ou executar testes.
        
5. **Runners**:
    
    - Servidores que executam os jobs. Podem ser gerenciados pelo GitHub (hosted runners) ou autogerenciados (self-hosted runners).
        

---

## Configuração Básica do GitHub Actions

### 1. Criar um Arquivo de Workflow

Os workflows são arquivos YAML localizados em `.github/workflows/`. Cada arquivo pode conter um ou mais jobs.

**Exemplo de Workflow Básico:**

```yml
name: CI Workflow

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout do código
        uses: actions/checkout@v3

      - name: Configurar Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'

      - name: Instalar dependências
        run: npm install

      - name: Rodar testes
        run: npm test
```

**Explicação:**

- `on`: Define os gatilhos do workflow (ex.: push e pull_request).
    
- `jobs`: Lista de jobs executados no workflow.
    
- `steps`: Etapas que compõem um job.
    

### 2. Configurar Gatilhos

Os gatilhos determinam quando o workflow será executado. Exemplos:

- `push`: Executa o workflow em pushes para branches específicas.
    
- `pull_request`: Executa em pull requests.
    
- `schedule`: Agendamento baseado em cron.
    

**Exemplo:**

```yml
on:
  push:
    branches:
      - main
  schedule:
    - cron: '0 0 * * *' # Executa diariamente à meia-noite
```

### 3. Usar Actions Predefinidas

Reaproveite ações disponíveis no GitHub Marketplace.

**Exemplo:**

- **Checkout do Código:**
    
    ```yml
    uses: actions/checkout@v3
    ```
    
- **Setup de Node.js:**
    
    ```yml
    uses: actions/setup-node@v3
    with:
      node-version: '16'
    ```
    

### 4. Executar Scripts Personalizados

Adicione comandos específicos para o seu projeto:

```
steps:
  - name: Rodar Linter
    run: npm run lint
```

---

## Funcionalidades Avançadas

### Matrizes de Configuração

Execute testes em diferentes configurações, como múltiplas versões do Node.js.

**Exemplo:**

```yml
jobs:
  test:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [14, 16, 18]

    steps:
      - name: Configurar Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}

      - name: Rodar testes
        run: npm test
```

### Armazenar Artefatos

Armazene arquivos gerados durante o workflow, como relatórios ou binários.

**Exemplo:**

```
- name: Armazenar relatórios
  uses: actions/upload-artifact@v3
  with:
    name: relatorio-teste
    path: test-report.xml
```

### Utilizar Secrets

Proteja informações sensíveis, como tokens de API, com o recurso de secrets.

**Configuração:**

1. Vá até o repositório no GitHub.
    
2. Acesse `Settings > Secrets and variables > Actions`.
    
3. Adicione um novo secret.
    

**Uso no Workflow:**

```
steps:
  - name: Usar Token
    env:
      TOKEN: ${{ secrets.MY_SECRET_TOKEN }}
    run: echo "Usando token $TOKEN"
```

### Paralelismo e Dependências

Os jobs podem ser executados em paralelo ou ter dependências.

**Exemplo:**

```
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Compilando projeto"

  test:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - run: echo "Rodando testes"
```

---

## Contexto de Boilerplate no GitHub Actions

### O que é um Boilerplate?

Um **boilerplate** é um conjunto de configurações ou templates padrão que podem ser reutilizados em vários projetos. No contexto do GitHub Actions, um boilerplate pode incluir workflows comuns, configurações de CI/CD e automações compartilhadas entre diferentes repositórios.

### Como Funciona um Boilerplate no GitHub Actions?

- **Templates Reutilizáveis**: Workflows comuns podem ser armazenados em um repositório central.
    
- **Reutilização via** `**uses**`: Você pode importar workflows de um repositório remoto para projetos específicos.
    
- **Padronização**: Garante que todos os projetos sigam práticas consistentes.
    

### Exemplo de Boilerplate Reutilizável

1. Crie um repositório dedicado a workflows.
    
    - Armazene templates em `.github/workflows`.
        
2. Exemplo de Workflow Boilerplate:
    

```
name: Build e Testes

on:
  push:
    branches:
      - main

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout do código
        uses: actions/checkout@v3

      - name: Configurar Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'

      - name: Instalar dependências
        run: npm install

      - name: Rodar testes
        run: npm test
```

3. Importar o Workflow para um Projeto:
    

```
name: CI Workflow

on: [push]

jobs:
  build:
    uses: organizacao/workflows/.github/workflows/build-and-test.yml@main
```

### Vantagens do Uso de Boilerplate

- **Eficiência**: Reduz o tempo necessário para configurar workflows em novos projetos.
    
- **Consistência**: Garante que todos os projetos utilizem configurações padronizadas.
    
- **Manutenção Centralizada**: Alterações podem ser feitas em um único lugar, afetando todos os projetos que utilizam o boilerplate.
    

### Melhores Práticas para Boilerplates

1. **Documentação Clara**: Inclua instruções detalhadas sobre como usar o boilerplate.
    
2. **Flexibilidade**: Permita que os projetos personalizem partes do workflow.
    
3. **Versionamento**: Use tags ou branches para controlar versões do boilerplate.
    

---

## Melhores Práticas

1. **Organização**:
    
    - Use nomes descritivos para jobs e steps.
        
2. **Reutilização**:
    
    - Armazene workflows comuns em templates reutilizáveis.
        
3. **Validação Prévia**:
    
    - Valide arquivos YAML com ferramentas como o VS Code e sua extensão YAML.
        
4. **Versionamento de Actions**:
    
    - Sempre especifique uma versão fixa de ações (ex.: `@v3`) para evitar problemas com atualizações.
        
5. **Feedback Rápido**:
    
    - Configure notificações para informar o status do workflow.
        

**Exemplo:**

```
steps:
  - name: Notificar Slack
    uses: slackapi/slack-github-action@v1.23.0
    with:
      slack-token: ${{ secrets.SLACK_TOKEN }}
      channel-id: 'C12345678'
      text: 'Workflow concluído!'
```

6. **Segurança**:
    
    - Minimize o uso de permissões elevadas nos workflows.
        
    - Use `permissions` para restringir o acesso.
        

**Exemplo:**

```
permissions:
  contents: read
  actions: none
```

---

## Resumo

O GitHub Actions é uma ferramenta poderosa que oferece CI/CD integrado e flexível para projetos GitHub. Com sua abordagem declarativa e extensibilidade, é possível criar fluxos de trabalho automatizados para uma ampla variedade de cenários, garantindo eficiência e qualidade no desenvolvimento de software.