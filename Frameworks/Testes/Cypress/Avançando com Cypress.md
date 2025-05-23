## 🧩 Comandos Essenciais com Exemplos Detalhados

### 🔄 `cy.reload()`
**O que faz?** Recarrega a página atual.  
**Casos de uso**: Testar persistência de dados após refresh, simular comportamento do usuário.  
```javascript
cy.get('#atualizar-dados').click()
cy.reload() // Recarrega a página
cy.get('.dados-atualizados').should('contain', 'Novo valor')
```

### 📦 `cy.wrap()`
**O que faz?** Transforma qualquer valor em um objeto Cypress para usar comandos encadeados.  
**Exemplo Prático**:
```javascript
const nome = 'Cypress'
cy.wrap(nome).should('equal', 'Cypress') // Transforma string em objeto testável

cy.get('li').then(($lista) => {
  cy.wrap($lista.first()).click() // Envolve elemento jQuery para usar comandos Cypress
})
```

### 🔄 `cy.each()`
**O que faz?** Itera sobre elementos de uma lista.  
**Exemplo Real**: Verificar todos os itens de uma lista de produtos
```javascript
cy.get('.lista-produtos li').each(($elemento, index) => {
  cy.wrap($elemento)
    .find('.preco')
    .should('contain', 'R$') // Verifica se todo produto tem preço
})
```

---

## 🛠 Comandos Avançados com Casos Reais

### 🔐 `cy.session()` (Autenticação Persistente)
**O que faz?** Mantém o estado de login entre testes (Cypress 10+).  
**Configuração em `cypress/support/e2e.js`**:
```javascript
beforeEach(() => {
  cy.session('login', () => {
    cy.visit('/login')
    cy.get('#email').type('user@test.com')
    cy.get('#senha').type('senha123')
    cy.get('#btn-login').click()
    cy.url().should('include', '/dashboard')
  })
})
```

### 📤 `cy.task()`
**O que faz?** Executa tarefas no Node.js (útil para limpar banco de dados, ler arquivos).  
**Configuração em `cypress.config.js`**:
```javascript
const { defineConfig } = require('cypress')

module.exports = defineConfig({
  e2e: {
    setupNodeEvents(on, config) {
      on('task', {
        limparBanco: () => {
          // Código para limpar o banco de dados
          return null
        }
      })
    }
  }
})
```
**No teste**:
```javascript
beforeEach(() => {
  cy.task('limparBanco') // Limpa dados antes de cada teste
})
```

### 🖼 Trabalhando com Iframes
**Desafio Comum**: Elementos dentro de iframes não são acessíveis diretamente.  
**Solução**:
```javascript
cy.get('#iframe-login').then(($iframe) => {
  const $body = $iframe.contents().find('body')
  cy.wrap($body)
    .find('#username')
    .type('usuario_teste')
  cy.wrap($body)
    .find('#password')
    .type('senha_secreta')
    .type('{enter}')
})
```

---

## 🧪 Exemplos Complexos Passo a Passo

### Exemplo 1: Teste de Upload de Arquivo
1. Instale o plugin:
```bash
npm install cypress-file-upload
```
2. Importe no `cypress/support/e2e.js`:
```javascript
import 'cypress-file-upload'
```
3. Teste:
```javascript
cy.get('#file-upload').attachFile('imagem-teste.jpg')
cy.get('#upload-status')
  .should('contain', 'Upload completo')
  .and('have.class', 'sucesso')
```

### Exemplo 2: Teste de API + UI Integrado
```javascript
// 1. Mock da API de produtos
cy.intercept('GET', '/api/produtos', { fixture: 'produtos.json' }).as('getProdutos')

// 2. Ação do usuário
cy.visit('/loja')
cy.wait('@getProdutos')

// 3. Validação UI + API
cy.get('.produto').should('have.length', 5)
cy.get('@getProdutos').its('response.body').should('have.property', 'destaque', true)
```

### Exemplo 3: Teste de Performance Básico
```javascript
cy.visit('/pagina-pesada')
cy.window().then((win) => {
  const medida = win.performance.timing
  const loadTime = medida.loadEventEnd - medida.navigationStart
  expect(loadTime).to.be.lessThan(2000) // Page load < 2 segundos
})
```

---

## 🕵️♂️ Debug Avançado: Técnicas de Investigação

### 1. **`cy.debug()` Contextual**
```javascript
cy.get('#form-complexo')
  .debug() // Pausa aqui para inspecionar o formulário
  .within(() => {
    cy.fillForm() // Comando personalizado
  })
```

### 2. **Console.log Estratégico**
```javascript
cy.get('.preco').then(($elemento) => {
  const preco = $elemento.text()
  console.log('Preço encontrado:', preco) // Aparece no DevTools
  cy.wrap(Number(preco.replace('R$ ', ''))
    .should('be.greaterThan', 100)
})
```

### 3. **Vídeo de Falhas**
Habilite no `cypress.config.js`:
```javascript
module.exports = defineConfig({
  e2e: {
    video: true, // Grava vídeo automaticamente
    videoCompression: 32 // Qualidade do vídeo
  }
})
```

---

## 🧠 Conhecimento Profundo: Como o Cypress Funciona?

### Arquitetura Única
| Componente | Função | Exemplo Prático |
|------------|--------|-----------------|
| **Driver do Cypress** | Comunica-se diretamente com o navegador | Quando você usa `cy.type()`, o Driver envia eventos reais de teclado |
| **Proxy** | Intercepta e modifica tráfego | `cy.intercept()` atua aqui para mockar APIs |
| **Node.js Server** | Gerencia testes e plugins | Quando você usa `cy.task()`, a comunicação acontece aqui |

### Ciclo de Vida de um Comando
1. **Enfileiramento**: `cy.get().click().type()` são enfileirados
2. **Execução**: Cypress executa cada comando em ordem
3. **Retry**: Se um elemento não é encontrado, Cypress tenta novamente até timeout
4. **Snapshot**: Tira foto do DOM após cada comando para o Time Travel

---

## 🛡 Padrões Anti-Frágeis (Flaky Tests)

### 1. **Seletores Resilientes**
```javascript
// ❌ Frágil (depende de classe CSS)
cy.get('.btn.btn-primary.mt-4')

// ✅ Resiliente (usa atributo data-test)
cy.get('[data-test="botao-salvar"]')
```

### 2. **Espera Inteligente**
```javascript
// ❌ Espera fixa (causa flakiness)
cy.wait(5000) // Nunca use!

// ✅ Espera dinâmica
cy.intercept('GET', '/api/dados').as('dadosCarregados')
cy.visit('/dashboard')
cy.wait('@dadosCarregados') // Espera até a API responder
```

### 3. **Testes Independentes**
```javascript
// ❌ Teste dependente do estado anterior
it('Teste 2 depende do Teste 1', () => { ... })

// ✅ Cada teste é auto-suficiente
beforeEach(() => {
  cy.limparBanco() // Garante estado limpo
  cy.login() // Recria estado necessário
})
```

---

## 🧩 Exercícios Práticos Expandidos

### Exercício 1: Formulário Dinâmico
1. Acesse [https://demoqa.com/automation-practice-form](https://demoqa.com/automation-practice-form)
2. Preencha todos os campos
3. Valide:
   - Modal de sucesso aparece
   - Todos dados submetidos estão corretos
   - Campo obrigatório vazio mostra erro

### Exercício 2: Carrinho de Compras
1. Mocke a API de produtos para retornar 3 itens
2. Simule:
   - Adição de 2 produtos ao carrinho
   - Remoção de 1 produto
   - Valide total calculado
3. Intercepte a API de checkout e verifique payload

### Exercício 3: Teste de Acessibilidade
1. Instale `cypress-axe`:
```bash
npm install cypress-axe
```
2. Configure em `cypress/support/e2e.js`:
```javascript
import 'cypress-axe'
```
3. Teste:
```javascript
cy.visit('/')
cy.injectAxe()
cy.checkA11y() // Valida regras de acessibilidade
```

---

## 🔧 Configurações Profissionais no `cypress.config.js`

```javascript
const { defineConfig } = require('cypress')

module.exports = defineConfig({
  e2e: {
    baseUrl: 'https://sua-aplicacao.com',
    defaultCommandTimeout: 10000, // Aumenta timeout padrão
    viewportWidth: 1920,
    viewportHeight: 1080,
    setupNodeEvents(on, config) {
      // Configura plugins aqui
      on('before:browser:launch', (browser, launchOptions) => {
        if (browser.name === 'chrome') {
          launchOptions.args.push('--disable-dev-shm-usage')
          return launchOptions
        }
      })
    },
    env: {
      usuario_admin: 'admin@test.com',
      senha_admin: 'S3nh4F0rt3!'
    }
  }
})
```

---

## 📜 Referência Completa de Comandos

| Comando | Uso | Exemplo |
|---------|-----|---------|
| `cy.clear()` | Limpa inputs | `cy.get('#email').clear()` |
| `cy.clearCookies()` | Remove cookies | `cy.clearCookies()` |
| `cy.clearLocalStorage()` | Limpa localStorage | `cy.clearLocalStorage()` |
| `cy.scrollTo()` | Rola a página | `cy.scrollTo('bottom')` |
| `cy.trigger()` | Dispara eventos | `cy.get('#elemento').trigger('mouseover')` |
| `cy.select()` | Seleciona em dropdown | `cy.get('#paises').select('Brasil')` |
| `cy.check()`/`cy.uncheck()` | Checkbox/radio | `cy.get('[type="checkbox"]').check()` |

---

## 🚨 Troubleshooting: Erros Comuns e Soluções

### **Problema**: Elemento não encontrado (`Timed out retrying`)
**Soluções**:
1. Verifique se o seletor está correto usando o Cypress Studio
2. Adicione espera para API relacionada:
```javascript
cy.intercept('GET', '/api/dados').as('carregamento')
cy.visit('/pagina')
cy.wait('@carregamento') // Espera dados carregarem
```
3. Aumente temporariamente o timeout:
```javascript
cy.get('.elemento-lento', { timeout: 15000 }).click()
```

### **Problema**: Teste passa local mas falha no CI
**Checklist**:
1. Verifique diferenças de ambiente (dados, timezone)
2. Habilite vídeo e screenshots no CI
3. Use containers Docker consistentes