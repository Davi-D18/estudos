
# Configuração de Husky, Commitlint e lint-staged

Este guia vai te ensinar a configurar as ferramentas **Husky**, **Commitlint** e **lint-staged** para automatizar o processo de validação e padronização do código no seu repositório. Vamos passar por cada uma das ferramentas e explicar como integrá-las corretamente.

## Índice

1. [Instalação do Husky](#instalacao-do-husky)
2. [Instalação do Commitlint](#instalacao-do-commitlint)
3. [Instalação do lint-staged](#instalacao-do-lint-staged)
4. [Integração das ferramentas com Husky](#integracao-das-ferramentas-com-husky)
5. [Exemplos e Dicas](#exemplos-e-dicas)

## 1. Instalação do Husky

O **Husky** é uma ferramenta que permite configurar hooks do Git para garantir que ações específicas sejam realizadas antes de cada commit ou push. Ele é extremamente útil para automatizar a execução de tarefas como validação de código, formatação e execução de testes.

### Passos para Instalar e Configurar o Husky

1. **Instalação do Husky**

   No terminal, execute o seguinte comando para instalar o Husky como dependência de desenvolvimento:

   ```bash
   npm install husky --save-dev
   ```

2. **Configuração do Husky**

   Adicione o script `prepare` no arquivo `package.json` para garantir que o Husky seja configurado automaticamente:

   ```json
   {
     "scripts": {
       "prepare": "husky install"
     }
   }
   ```

3. **Rodando o script prepare**

   Após a instalação, execute o comando a seguir para preparar os hooks do Husky:

   ```bash
   npm run prepare
   ```

   Isso criará um diretório `.husky` no seu projeto.

### O que são hooks do Git?

Os **Git hooks** são scripts que permitem automatizar tarefas no processo de commit, push e outras ações no Git. Com o Husky, você pode configurar esses hooks facilmente. Alguns exemplos de hooks incluem:

- `pre-commit`: Executa antes de um commit ser finalizado.
- `commit-msg`: Executa após a criação da mensagem de commit.
- `pre-push`: Executa antes de um push ser feito.

## 2. Instalação do Commitlint

O **Commitlint** é utilizado para garantir que as mensagens de commit sigam um padrão, como o [Conventional Commits](https://www.conventionalcommits.org/). Isso ajuda a manter um histórico de commits mais organizado e facilita a integração com outras ferramentas, como o Semantic Release.

### Passos para Instalar e Configurar o Commitlint

1. **Instalação do Commitlint**

   Execute o seguinte comando para instalar o Commitlint e a configuração padrão dos commits:

   ```bash
   npm install @commitlint/cli @commitlint/config-conventional --save-dev
   ```

2. **Configuração do Commitlint**

   Crie um arquivo `commitlint.config.js` na raiz do projeto com o seguinte conteúdo:

   ```javascript
   module.exports = { extends: ['@commitlint/config-conventional'] };
   ```

3. **Integração do Commitlint com Husky**

   Adicione o hook `commit-msg` no Husky para validar a mensagem de commit:

   ```bash
   npx husky add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'
   ```

   Esse hook irá garantir que as mensagens de commit estejam em conformidade com o padrão definido no Commitlint.

### Exemplos de Mensagens de Commit

Mensagens de commit seguindo o padrão do **Conventional Commits** podem ser:

- `feat: adicionar página de contato`
- `fix: corrigir bug de validação`
- `chore: atualizar dependências`

Saiba mais sobre os tipos de mensagens em [Conventional Commits](https://www.conventionalcommits.org/).

## 3. Instalação do lint-staged

O **lint-staged** é uma ferramenta que permite rodar linters e formatadores apenas nos arquivos que estão prestes a ser commitados. Isso economiza tempo e evita que você execute linters em arquivos que não foram modificados.

### Passos para Instalar e Configurar o lint-staged

1. **Instalação do lint-staged**

   Execute o seguinte comando para instalar o lint-staged como dependência de desenvolvimento:

   ```bash
   npm install lint-staged --save-dev
   ```

2. **Configuração do lint-staged**

   Adicione a seguinte configuração no arquivo `package.json`:

   ```json
   {
     "lint-staged": {
       "*.js": ["eslint --fix", "git add"],
       "*.css": ["stylelint --fix", "git add"]
     }
   }
   ```

   Esse exemplo configura o lint-staged para rodar o ESLint e Stylelint nos arquivos `.js` e `.css`, respectivamente, corrigindo-os automaticamente antes de serem commitados.

## 4. Integração das Ferramentas com Husky

Agora que você já tem o Husky, Commitlint e lint-staged instalados, vamos integrá-los:

1. **Configuração do hook `pre-commit` para lint-staged**

   Adicione o seguinte comando no arquivo `.husky/pre-commit` para rodar o lint-staged antes de cada commit:

   ```bash
   npx husky add .husky/pre-commit 'npx lint-staged'
   ```

2. **Configuração do hook `commit-msg` para Commitlint**

   Como já visto anteriormente, adicione a seguinte configuração no arquivo `.husky/commit-msg`:

   ```bash
   npx husky add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'
   ```

Com isso, seus hooks estarão configurados para validar a mensagem de commit e rodar os linters apenas nos arquivos modificados.

## 5. Exemplos e Dicas

### Exemplos de Configuração de Hooks

Aqui estão alguns exemplos de hooks que você pode adicionar ao seu projeto:

- **Pre-commit (lint-staged)**: Executa linters nos arquivos modificados antes de um commit.
  ```bash
  npx husky add .husky/pre-commit 'npx lint-staged'
  ```

- **Commit-msg (Commitlint)**: Valida a mensagem de commit com base no padrão definido.
  ```bash
  npx husky add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'
  ```

### Dicas para uma boa organização de commits:

- Sempre escreva mensagens de commit claras e concisas.
- Siga o padrão de Conventional Commits para facilitar a automação de versões e releases.
- Use o lint-staged para otimizar o tempo de execução de linters, aplicando-os apenas nos arquivos modificados.

## Links Úteis

- [Husky Documentation](https://typicode.github.io/husky/)
- [Commitlint Documentation](https://commitlint.js.org/#/)
- [lint-staged Documentation](https://github.com/okonet/lint-staged)

---

Agora, seu fluxo de trabalho com Git estará mais eficiente e padronizado, melhorando a qualidade do código no seu repositório.