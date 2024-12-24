
# Instalação e Configuração do ESLint, Prettier e EditorConfig

Aqui está um guia detalhado e simples para configurar **ESLint**, **Prettier** e **EditorConfig** no seu projeto.

---

## **1. Configurando o ESLint**

### **O que é o ESLint?**
O **ESLint** é uma ferramenta que analisa seu código JavaScript (ou TypeScript) para encontrar problemas, como erros de sintaxe ou estilos inconsistentes. Ele ajuda a padronizar o código e evitar erros comuns.

### **Por que usar?**
- Ajuda a encontrar problemas antes de executar o código.
- Mantém um padrão de estilo no projeto.
- Pode corrigir automaticamente pequenos problemas.

### **Passos para Configuração**

1. **Instale o ESLint no projeto**:
   ```bash
   npm install eslint --save-dev
   ```

2. **Inicie a configuração**:
   ```bash
   npx eslint --init
   ```

   Durante o processo, você verá perguntas como:
   - **Como você deseja usar o ESLint?**  
     Escolha: "To check syntax, find problems, and enforce code style".

   - **Tipo de módulo**:  
     Escolha entre `JavaScript Modules (import/export)` ou `CommonJS (require/export)`.

   - **Framework**:  
     Selecione o framework que está usando (React, Vue, etc.) ou "None".

   - **Onde rodará o código?**  
     Escolha entre "Browser", "Node.js" ou ambos.

   - **Instalar dependências?**  
     Escolha "Sim" para instalar automaticamente os pacotes necessários.

3. **Arquivo `.eslintrc.json`**  
   Após isso, será criado um arquivo de configuração chamado `.eslintrc.json` com as regras escolhidas.

4. **Exemplo de Configuração**:
   ```json
   {
     "env": {
       "browser": true,
       "es2021": true
     },
     "extends": "eslint:recommended",
     "parserOptions": {
       "ecmaVersion": 12,
       "sourceType": "module"
     },
     "rules": {
       "semi": ["error", "always"],
       "quotes": ["error", "double"]
     }
   }
   ```

---

## **2. Configurando o Prettier com ESLint**

### **O que é o Prettier?**
O **Prettier** é uma ferramenta de formatação de código. Ele ajusta automaticamente a aparência do código, como espaçamento, indentação e aspas.

### **Por que usar Prettier com ESLint?**
- **ESLint** cuida de erros e padrões de estilo mais complexos.
- **Prettier** garante a formatação consistente e uniforme.

### **Instalação**

1. Instale o Prettier e os plugins necessários para integração com o ESLint:
   ```bash
   npm install prettier eslint-config-prettier eslint-plugin-prettier --save-dev
   ```

2. Atualize o arquivo `.eslintrc.json` para usar o Prettier junto com o ESLint:
   ```json
   {
     "extends": [
       "eslint:recommended",
       "plugin:prettier/recommended"
     ],
     "rules": {
       "prettier/prettier": "error"
     }
   }
   ```

3. Crie um arquivo `.prettierrc` para definir regras do Prettier:
   ```json
   {
     "semi": true,
     "singleQuote": true,
     "tabWidth": 2,
     "trailingComma": "es5"
   }
   ```

4. Crie um arquivo `.prettierignore` para ignorar arquivos:
   ```
   node_modules/
   dist/
   ```

---

## **3. Configurando o EditorConfig**

### **O que é o EditorConfig?**
O **EditorConfig** ajuda a manter o mesmo estilo de formatação entre diferentes editores de texto. Isso é útil quando várias pessoas trabalham no mesmo projeto.

### **Instalação**
- Instale o plugin **EditorConfig** no seu editor (VS Code, IntelliJ, etc.).

### **Configuração**
1. Crie um arquivo `.editorconfig` na raiz do projeto:
   ```ini
   root = true

   [*]
   indent_style = space
   indent_size = 2
   end_of_line = lf
   charset = utf-8
   trim_trailing_whitespace = true
   insert_final_newline = true
   ````

2. O que cada regra faz:
   - **`indent_style`**: Define se a indentação usa espaços ou tabs.
   - **`indent_size`**: Tamanho da indentação (ex.: 2 espaços).
   - **`end_of_line`**: Usa linhas terminadas com LF (Linux) ou CRLF (Windows).
   - **`charset`**: Codificação de caracteres (UTF-8).
   - **`trim_trailing_whitespace`**: Remove espaços no final das linhas.
   - **`insert_final_newline`**: Adiciona uma nova linha no final dos arquivos.

---

## **4. Automatizando Tudo**

### **Executar ESLint e Prettier Manualmente**
- Para corrigir problemas com o ESLint:
  ```bash
  npx eslint . --fix
  ```

- Para formatar com o Prettier:
  ```bash
  npx prettier --write .
  ```

### **Automatizar no Git com Husky e lint-staged**
1. Instale as dependências:
   ```bash
   npm install husky lint-staged --save-dev
   ```

2. Configure o `package.json`:
   ```json
   "lint-staged": {
     "*.{js,jsx,ts,tsx}": [
       "eslint --fix",
       "prettier --write"
     ]
   }
   ```

3. Adicione o hook `pre-commit`:
   ```bash
   npx husky add .husky/pre-commit "npx lint-staged"
   ```

---

## **5. Arquivos Criados no Projeto**
- **`.eslintrc.json`**: Regras do ESLint.
- **`.prettierrc`**: Regras do Prettier.
- **`.editorconfig`**: Regras universais para editores.
- **`.prettierignore`**: Ignora arquivos do Prettier.
- **`.eslintignore`**: Ignora arquivos do ESLint.

---

## **Dicas e Boas Práticas**
- Sempre teste suas configurações rodando o ESLint e Prettier manualmente antes de automatizar.
- Use o **EditorConfig** para evitar problemas de formatação em times.

---
