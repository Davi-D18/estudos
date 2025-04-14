## **O que é JSDOM?**

O JSDOM é uma biblioteca JavaScript que permite simular um DOM (Document Object Model) completo no ambiente Node.js. Ele transforma uma string HTML em um DOM funcional, permitindo que você use métodos como `querySelector`, `getElementById` e outros para manipular e acessar elementos de uma página, como se estivesse em um navegador.

Isso é útil em situações onde você precisa extrair dados de páginas web (scraping) e realizar manipulações que seriam feitas no frontend de um site.

---

## **Instalando o JSDOM**

Antes de começar, você precisa instalar o JSDOM em seu projeto. Para isso, execute o seguinte comando:

```bash
npm install jsdom
```

Se você usa Yarn:

```bash
yarn add jsdom
```

---

## **Montando o Scrapper**

### 1. **Obter o HTML da Página**

Você pode usar uma biblioteca como `axios` para fazer uma requisição HTTP e obter o HTML da página. Por exemplo:

```javascript
const axios = require("axios");

async function fetchHTML(url) {
  const response = await axios.get(url);
  return response.data; // Retorna o HTML da página como string
}
```

### 2. **Transformar o HTML em DOM**

Agora, use o JSDOM para transformar o HTML obtido em um DOM manipulável:

```javascript
const { JSDOM } = require("jsdom");

async function createDOM(html) {
  const dom = new JSDOM(html);
  return dom.window.document;
}
```

### 3. **Selecionar e Extrair Dados**

Use métodos como `querySelector` ou `querySelectorAll` para localizar elementos na página e extrair os dados desejados.

```javascript
async function extractGameData(url) {
  // 1. Obter o HTML da página
  const html = await fetchHTML(url);

  // 2. Criar o DOM
  const document = await createDOM(html);

  // 3. Selecionar elementos e extrair dados
  const descriptionElement = document.querySelector(".description");
  const description = descriptionElement?.textContent.trim() || "Descrição não encontrada";

  const ratingElement = document.querySelector(".rating-icon");
  const rating = ratingElement?.getAttribute("data-rating") || "0";

  return {
    description,
    rating,
  };
}
```

### 4. **Testando o Scrapper**

Chame a função passando a URL desejada e exiba os dados extraídos:

```javascript
(async () => {
  const url = "https://example.com/game/slug"; // Substitua pela URL real
  const gameData = await extractGameData(url);

  console.log(gameData);
})();
```

---

## **Exemplo Completo**

Aqui está o código completo:

```javascript
const axios = require("axios");
const { JSDOM } = require("jsdom");

async function fetchHTML(url) {
  const response = await axios.get(url);
  return response.data;
}

async function createDOM(html) {
  const dom = new JSDOM(html);
  return dom.window.document;
}

async function extractGameData(url) {
  const html = await fetchHTML(url);
  const document = await createDOM(html);

  const descriptionElement = document.querySelector(".description");
  const description = descriptionElement?.textContent.trim() || "Descrição não encontrada";

  const ratingElement = document.querySelector(".rating-icon");
  const rating = ratingElement?.getAttribute("data-rating") || "0";

  return {
    description,
    rating,
  };
}

(async () => {
  const url = "https://example.com/game/slug"; // Substitua pela URL real
  const gameData = await extractGameData(url);

  console.log(gameData);
})();
```

---

## **Recursos Avançados**

1. **Tratamento de Erros**: Certifique-se de usar `try-catch` para lidar com erros ao fazer requisições ou manipular o DOM.
2. **Paginação**: Se você precisa percorrer várias páginas, pode iterar sobre uma lista de URLs ou parâmetros de consulta.
3. **Customização**: Você pode adicionar lógica para limpar ou formatar os dados antes de retornar.

---

## **Conclusão**

Com o JSDOM, você pode criar um scrapper poderoso e flexível para extrair dados de páginas web, mesmo quando elas não fornecem APIs diretas. Combine isso com bibliotecas como `axios` para manipular HTML dinâmico e construir soluções eficazes de scraping.