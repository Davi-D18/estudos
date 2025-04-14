### **Visão Geral**

Este guia aborda como implementar upload de imagens no Strapi v5, incluindo a criação de imagens de capa (**Cover**) e galerias (**Gallery**) para jogos. Ele utiliza buffers para processar as imagens e a biblioteca **Axios** para realizar requisições HTTP, permitindo um fluxo automatizado de upload.

---

### **Upload de Imagens no Strapi**

#### **1. Contexto**

No Strapi, o upload de imagens é realizado associando arquivos a um modelo específico, como jogos, através de campos como `cover` e `gallery`. Para fazer o upload programaticamente:

1. A imagem é obtida via requisição HTTP e transformada em buffer.
    
2. Um `FormData` é criado para conter os dados da imagem e suas referências.
    
3. O upload é feito para a API do Strapi.
    

#### **2. Configuração de Permissões**

Para que o upload funcione, é necessário habilitar o recurso na configuração de permissões:

1. Acesse **Settings > Users & Permissions > Roles**.
    
2. Na aba **Public**, habilite a permissão para **Upload**.
    
3. Salve as alterações.
    

---

### **Função** `**setImage**`

A função `setImage` realiza o upload de uma imagem para o Strapi.

#### **Código**:

```js
async function setImage({ image, game, field = "cover" }) {
  const { data } = await axios.get(image, { responseType: "arraybuffer" });
  const buffer = Buffer.from(data, "base64");

  const FormData = require("form-data");
  const formData = new FormData();

  formData.append("refId", game.id); // ID do jogo associado
  formData.append("ref", "api::game.game"); // Referência ao modelo de jogo
  formData.append("field", field); // Campo onde a imagem será salva
  formData.append("files", buffer, { filename: `${game.slug}.jpg` });

  console.info(`Uploading ${field} image: ${game.slug}.jpg`);

  await axios({
    method: "POST",
    url: `http://localhost:1337/api/upload/`,
    data: formData,
    headers: {
      "Content-Type": `multipart/form-data; boundary=${formData._boundary}`,
    },
  });
}
```

#### **Fluxo**:

1. A imagem é baixada da URL fornecida e convertida para buffer.
    
2. Um objeto `FormData` é criado contendo as referências ao modelo e ao campo.
    
3. O upload é realizado para a API de upload do Strapi.
    

---

### **Atualizando o** `**createGames**` **para Suportar Upload de Imagens**

A função `createGames` é modificada para incluir chamadas à `setImage`:

#### **Código**:

```js
async function createGames(products) {
  await Promise.all(
    products.map(async (product) => {
      const item = await getByName(product.title, "api::game.game");

      if (!item) {
        console.info(`Creating: ${product.title}...`);

        const game = await strapi.service("api::game.game").create({
          data: {
            name: product.title,
            slug: product.slug,
            price: product.price.finalMoney.amount,
            release_date: new Date(product.releaseDate),
            categories: await Promise.all(
              product.genres.map(({ name }) => getByName(name, "api::category.category"))
            ),
            platforms: await Promise.all(
              product.operatingSystems.map((name) => getByName(name, "api::platform.platform"))
            ),
            developers: await Promise.all(
              product.developers.map((name) => getByName(name, "api::developer.developer"))
            ),
            publisher: await Promise.all(
              product.publishers.map((name) => getByName(name, "api::publisher.publisher"))
            ),
            ...(await getGameInfo(product.slug)),
            publishedAt: new Date(),
          },
        });

        // Upload da imagem de capa
        await setImage({ image: product.coverHorizontal, game });

        // Upload das imagens da galeria
        await Promise.all(
          product.screenshots.slice(0, 5).map((url) =>
            setImage({
              image: `${url.replace("{formatter}", "product_card_v2_mobile_slider_639")}`,
              game,
              field: "gallery",
            })
          )
        );

        return game;
      }
    })
  );
}
```

#### **Fluxo**:

1. Cria o jogo no banco de dados usando `strapi.service().create`.
    
2. Faz o upload da capa usando `setImage`.
    
3. Faz o upload de até 5 imagens da galeria, ajustando a URL com `replace` para o formato correto.
    

---

### **Resumo**

- `**setImage**`: Realiza o upload de imagens associando-as a um campo específico de um modelo no Strapi.
    
- `**createGames**`: Inclui as chamadas a `setImage` para processar e fazer upload das imagens de capa e galeria.
    
- **Permissões**: Certifique-se de habilitar o upload nas permissões da API.
    
- **Uso de Axios**: Facilita o download e upload das imagens.
    
- **Buffer**: Converte os dados da imagem para um formato adequado para upload.
    

Com essa implementação, é possível gerenciar facilmente imagens associadas a jogos ou outros modelos no Strapi, automatizando o processo e garantindo que as imagens sejam corretamente vinculadas e armazenadas.