### **Visão Geral**

Este guia aborda como realizar scraping de dados utilizando **JSDOM** e integrá-los ao **Strapi v5** por meio de serviços personalizados. O exemplo foca em consumir a API da **GOG (Good Old Games)** para buscar informações sobre jogos e população do banco de dados com entidades relacionadas.

---

### **O que é o JSDOM?**

- **Definição**: O JSDOM é uma biblioteca que simula o DOM (Document Object Model) em ambientes Node.js. Ele permite manipular HTML como se estivesse em um navegador, utilizando seletores CSS, atributos, e outros.
    
- **Como funciona?**: Transformando strings de HTML em objetos manipuláveis por JavaScript.
    

#### **Exemplo Simples de Uso**

```js
import { JSDOM } from "jsdom";

const html = `<div class="description">Descrição do Jogo</div>`;
const dom = new JSDOM(html);

const description = dom.window.document.querySelector(".description").textContent;
console.log(description); // "Descrição do Jogo"
```

---

### **Passos para Integração com o Strapi**

#### **1. Criando o Serviço de Scraping no Strapi**

Um serviço personalizado é criado para realizar o scraping e manipular dados obtidos da API externa. Neste exemplo, utilizamos o serviço de jogos (`game`):

```js
import { factories } from "@strapi/strapi";
import axios from "axios";
import { JSDOM } from "jsdom";

export default factories.createCoreService("api::game.game", () => ({
  async populate() {
    const gogApiUrl = "https://catalog.gog.com/v1/catalog?limit=48&order=desc%3Atrending";

    const { data: { products } } = await axios.get(gogApiUrl);

    // Exemplo de processamento de produtos
    console.log(products);
  },
}));
```

#### **2. Obtendo Dados com Axios**

- Fazemos requisições HTTP para APIs externas utilizando **Axios**.
    
- **Exemplo**:
    

```js
const response = await axios.get("https://api.example.com/data");
console.log(response.data);
```

#### **3. Processando o DOM com JSDOM**

Extraímos dados relevantes do HTML de uma página:

```js
async function getGameInfo(slug) {
  const gogSlug = slug.replaceAll("-", "_").toLowerCase();
  const body = await axios.get(`https://www.gog.com/game/${gogSlug}`);
  const dom = new JSDOM(body.data);

  const raw_description = dom.window.document.querySelector(".description");

  return {
    description: raw_description.innerHTML,
    short_description: raw_description.textContent.slice(0, 160),
  };
}
```

---

### **Criando Relacionamentos Many-to-Many**

#### **1. Função** `**createManyToManyData**`

Essa função cria entidades relacionadas, como developers, publishers, categorias e plataformas:

```js
async function createManyToManyData(products) {
  const developersSet = new Set();
  const publishersSet = new Set();
  const categoriesSet = new Set();
  const platformsSet = new Set();

  products.forEach((product) => {
    const { developers, publishers, genres, operatingSystems } = product;

    genres?.forEach(({ name }) => categoriesSet.add(name));
    operatingSystems?.forEach((os) => platformsSet.add(os));
    developers?.forEach((dev) => developersSet.add(dev));
    publishers?.forEach((pub) => publishersSet.add(pub));
  });

  const createCall = (set, entityService) =>
    Array.from(set).map((name) => create(name, entityService));

  return Promise.all([
    ...createCall(developersSet, "api::developer.developer"),
    ...createCall(publishersSet, "api::publisher.publisher"),
    ...createCall(categoriesSet, "api::category.category"),
    ...createCall(platformsSet, "api::platform.platform"),
  ]);
}
```

#### **2. Função** `**create**`

Garante que entidades não sejam duplicadas:

```js
async function create(name, entityService) {
  const item = await strapi.service(entityService).find({ filters: { name } });

  if (!item.results.length) {
    await strapi.service(entityService).create({
      data: {
        name,
        slug: slugify(name, { strict: true, lower: true }),
      },
    });
  }
}
```

---

### **Criando Jogos no Banco de Dados**

#### **Função** `**createGames**`

Popula os dados dos jogos e relaciona com as entidades criadas:

```js
async function createGames(products) {
  await Promise.all(
    products.map(async (product) => {
      const item = await strapi.service("api::game.game").find({ filters: { name: product.title } });

      if (!item.results.length) {
        await strapi.service("api::game.game").create({
          data: {
            name: product.title,
            slug: product.slug,
            price: product.price.finalMoney.amount,
            release_date: new Date(product.releaseDate),
            categories: await Promise.all(
              product.genres.map(({ name }) => getByName(name, "api::category.category"))
            ),
            platforms: await Promise.all(
              product.operatingSystems.map((os) => getByName(os, "api::platform.platform"))
            ),
            developers: await Promise.all(
              product.developers.map((dev) => getByName(dev, "api::developer.developer"))
            ),
            publisher: await Promise.all(
              product.publishers.map((pub) => getByName(pub, "api::publisher.publisher"))
            ),
          },
        });
      }
    })
  );
}
```

---

### **Fluxo Geral da População**

1. **Obter dados da API da GOG**.
    
2. **Criar entidades relacionadas**:
    
    - Developers
        
    - Publishers
        
    - Categorias
        
    - Plataformas
        
3. **Criar jogos com dados e relacionamentos**:
    
    - Nome, descrição, preço, data de lançamento, etc.
        

---

### **Conclusão**

Este guia apresenta uma abordagem completa para scraping e população de dados no Strapi v5 utilizando o JSDOM. Ele combina boas práticas, organização em serviços e a manipulação de relações many-to-many. Com este modelo, você pode facilmente adaptar o código para outras aplicações ou fontes de dados.