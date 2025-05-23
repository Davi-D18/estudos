## 🧩 O Que é Cypress e Por Que Usar?

### 🤔 **Pra Que Serve?**
Imagine que você quer testar se um usuário consegue:
1. Fazer login
2. Adicionar um produto ao carrinho
3. Finalizar a compra

O Cypress **automatiza esses passos** como um usuário real faria, mas 10x mais rápido!

### ✨ **Vantagens

| Funcionalidade | Exemplo Prático |
|----------------|-----------------|
| **Recarregamento Automático** | Edita o teste → Salva → Cypress roda novamente automaticamente |
| **Time Travel** | Veja snapshots de cada passo do teste após a execução |
| **Espera Inteligente** | Não precisa usar `setTimeout` – Cypress espera elementos aparecerem sozinho |

### ❌ **O Que Cypress Não Faz?**
- Testes em **aplicativos mobile nativos** (use Appium)
- Testes em **múltiplas janelas** simultaneneas

---

## 🛠 Configurando Seu Primeiro Projeto

### Passo a Passo para Iniciantes
1. Crie uma pasta para seu projeto:
   ```bash
   mkdir meu-primeiro-teste
   cd meu-primeiro-teste
   ```
2. Inicie um projeto Node.js (cria o `package.json`):
   ```bash
   npm init -y
   ```
3. Instale o Cypress:
   ```bash
   npm install cypress --save-dev
   ```
4. Abra o Cypress:
   ```bash
   npx cypress open
   ```

🔍 **O Que Aconteceu?**  
O Cypress criou automaticamente:
- `cypress/e2e/`: Onde seus testes moram
- `cypress/fixtures/`: Dados fixos (ex: mock de API)
- `cypress/support/`: Configurações globais

👉 **Experimente!** Rode o teste exemplo em `cypress/e2e/example.cy.js` para ver a mágica acontecer.

---

## 🎯 Dominando os Comandos Básicos

### 1. `cy.visit()` – Sua Porta de Entrada
```javascript
cy.visit('https://www.google.com') // Navega para o Google
```
⚠️ **Cuidado!** Sempre use URLs completas (`https://`) ou configure `baseUrl` no `cypress.config.js`.

### 2. `cy.get()` – Encontre Elementos Como um Caçador
```javascript
// Por ID
cy.get('#login-button')

// Por Classe
cy.get('.submit-btn')

// Por Atributo
cy.get('[data-test="search-input"]')
```
💡 **Dica Pro:** Use `data-test` em vez de classes/IDs – evita quebras quando o CSS muda!

### 3. `cy.type()` – Digitando Como um Datilógrafo
```javascript
cy.get('#email')
  .type('teste@exemplo.com') // Digita normalmente
  .type('{backspace}') // Apaga o último caractere
  .type('teste@exemplo.com.br') // Completa o email
```
📌 **Teclas Especiais:**  
`{enter}`, `{esc}`, `{pageUp}`, etc. Veja a [lista completa](https://docs.cypress.io/api/commands/type#Arguments).

### 4. `cy.click()` – Clicando com Precisão
```javascript
cy.get('#submit-btn').click() // Clica no botão
cy.contains('Confirmar').click() // Clica no texto "Confirmar"
```

### 🎓 **Exercício Prático 1**  
Crie um teste que:
1. Visite [https://demoqa.com/text-box](https://demoqa.com/text-box)
2. Preencha todos os campos
3. Clique em "Submit"

---

## 🔍 Asserções: Como Validar Seu Teste

### `should()` – Seu Detetive Particular
```javascript
// Verifica se o elemento está visível
cy.get('.success-message').should('be.visible')

// Verifica se contém texto
cy.get('#title').should('contain', 'Bem-vindo')

// Verifica CSS
cy.get('.alert').should('have.css', 'color', 'rgb(255, 0, 0)')
```

### Comparando `should()` vs `expect()`
| `should()` | `expect()` |
|------------|------------|
| Asserções encadeadas | Asserções em variáveis |
| Espera automática | Precisa de `then()` |
| **Exemplo:** | **Exemplo:** |
| ```cy.get('.list').should('have.length', 5)``` | ```cy.get('.list').then(($el) => { expect($el).to.have.length(5) })``` |

### 🛑 **Erros Comuns de Iniciantes**
```javascript
// ❌ Ruim (elemento pode não existir ainda)
expect(cy.get('#elemento')).to.exist

// ✅ Bom (encadeamento correto)
cy.get('#elemento').should('exist')
```

---

## 🧪 Comandos Intermediários para Testes Realistas

### Mockando APIs com `cy.intercept()`
Simule uma API que retorna erro 500:
```javascript
cy.intercept('GET', '/api/produtos', {
  statusCode: 500,
  body: { erro: 'Serviço indisponível' }
}).as('getProdutos')

// No teste:
cy.visit('/produtos')
cy.wait('@getProdutos')
cy.get('.erro-api').should('contain', 'Tente novamente mais tarde')
```

### Trabalhando com Arquivos (`cy.fixture()`)
`cypress/fixtures/usuario.json`:
```json
{
  "nome": "Ana Silva",
  "email": "ana@exemplo.com"
}
```
No teste:
```javascript
cy.fixture('usuario.json').then((usuario) => {
  cy.get('#nome').type(usuario.nome)
  cy.get('#email').type(usuario.email)
})
```

---

## 🚀 Técnicas Avançadas como um Pro

### 1. **Testes Paralelos**
Configure no `cypress.config.js`:
```javascript
module.exports = defineConfig({
  e2e: {
    experimentalRunAllSpecs: true // Roda todos specs em paralelo
  }
})
```

### 2. **Autenticação sem UI**
Crie um comando personalizado em `cypress/support/commands.js`:
```javascript
Cypress.Commands.add('loginAPI', (email, senha) => {
  cy.request('POST', '/api/login', { email, senha }).then((res) => {
    localStorage.setItem('token', res.body.token)
  })
})
```
No teste:
```javascript
beforeEach(() => {
  cy.loginAPI('teste@exemplo.com', 'senha123')
})
```

---

## 🐞 Debugando Testes como um Detetive

### Ferramentas Nativas
1. **`cy.pause()`**  
   Pausa o teste até você clicar em "Resume"
   ```javascript
   cy.get('#btn').click()
   cy.pause() // Teste para aqui!
   cy.get('.modal').should('be.visible')
   ```

2. **`cy.debug()`**  
   Mostra o estado atual do elemento no console
   ```javascript
   cy.get('#formulario').debug() // Console.log automático
   ```

3. **Time Travel**  
   Clique em qualquer passo no Test Runner para ver como a página estava naquele momento!

---

## 🏆 Boas Práticas para Evitar Dor de Cabeça

### 1. **Seletores à Prova de Mudanças**
Ruim ❌:
```html
<button class="btn btn-primary">Salvar</button>
```
Bom ✅:
```html
<button data-test="salvar-perfil">Salvar</button>
```
No teste:
```javascript
cy.get('[data-test="salvar-perfil"]')
```

### 2. **Organização de Testes**
Estrutura recomendada:
```
cypress/
├─ e2e/
│  ├─ login/
│  │  ├─ sucesso.cy.js
│  │  ├─ erro.cy.js
│  ├─ carrinho/
│  │  ├─ adicionar.cy.js
```

### 3. **Evite Condicionais em Testes**
Ruim ❌:
```javascript
if (usuarioLogado) {
  cy.get('.perfil').click()
}
```
Bom ✅:
```javascript
// Crie dois testes separados
// 1. Teste com usuário logado
// 2. Teste sem login
```

---

## 📈 Recursos para Continuar Aprendendo

### Cursos Recomendados
- [Cypress Discovery](https://qacademy.io/cypress) (Português)
- [Cypress.io Official Courses](https://cypress.io/training) (Inglês)

### Projetos para Praticar
1. [DemoQA](https://demoqa.com) - Site perfeito para testes básicos
2. [Saucedemo](https://saucedemo.com) - E-commerce fictício para testes complexos

### Comunidades
- [Discord Cypress Brasil](https://discord.gg/cypress-br)
- [Fórum Oficial](https://github.com/cypress-io/cypress/discussions)

---

✨ **Desafio Final**: Crie um teste que verifique o fluxo completo de compra em um e-commerce, incluindo:
- Login
- Seleção de produto
- Checkout
- Validação do pedido