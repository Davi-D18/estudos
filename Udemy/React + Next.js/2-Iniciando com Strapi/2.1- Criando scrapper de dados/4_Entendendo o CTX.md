## Entendendo o ctx no Strapi

### 1. O que é o ctx?

**Definição:**
O `ctx` é a abreviação de "context" (contexto) e é um objeto utilizado no Strapi para gerenciar requisições e respostas dentro dos controllers. Ele serve como um ponto central para acessar informações tanto sobre a requisição (request) quanto sobre a resposta (response).

**Origem:**
O Strapi utiliza o Koa, um framework Node.js, para lidar com requisições e respostas. O `ctx` é herdado diretamente do Koa, agrupando todas as informações da requisição e da resposta em um único objeto.

### 2. Estrutura do ctx

O objeto `ctx` possui duas divisões principais:

- **Request:** Contém dados relacionados à requisição feita pelo cliente.
- **Response:** Contém dados e métodos relacionados à resposta que será enviada ao cliente.

**Exemplos de propriedades importantes no ctx:**

**Request (requisição):**
- `ctx.query`: Parâmetros de busca enviados na URL (Query Parameters).
- `ctx.params`: Parâmetros de rota (como `/games/:id`).
- `ctx.request.body`: Dados enviados no corpo da requisição (como no método POST).
- `ctx.url`: URL completa da requisição.
- `ctx.method`: Método HTTP utilizado (GET, POST, PUT, DELETE, etc.).

**Response (resposta):**
- `ctx.status`: Código de status HTTP da resposta (ex.: 200, 404, 500).
- `ctx.body`: Corpo da resposta que será enviado ao cliente.
- `ctx.send()`: Método para enviar uma resposta ao cliente.

### 3. Como usar o ctx na prática?

#### 3.1. Acessando Query Parameters

Query Parameters são informações enviadas na URL após o símbolo `?`. Por exemplo: `/games?sort=popularity&page=1`.

**Exemplo no Strapi:**

```javascript
export default {
  async getGames(ctx) {
    // Acessando os Query Parameters
    const { sort, page } = ctx.query;

    console.log('Query Parameters:', ctx.query);
    
    // Retornando a resposta com os parâmetros
    ctx.send({ message: `Sort: ${sort}, Page: ${page}` });
  },
};
```

**Resultado esperado:**
Se o cliente acessar `/games?sort=popularity&page=1`, no console será exibido:
```json
Query Parameters: { sort: "popularity", page: "1" }
```
A resposta será:
```json
{ "message": "Sort: popularity, Page: 1" }
```

#### 3.2. Acessando o Corpo da Requisição

O corpo da requisição é comumente usado em métodos como POST e PUT para enviar dados do cliente para o servidor.

**Exemplo no Strapi:**

```javascript
export default {
  async createGame(ctx) {
    // Acessando o corpo da requisição
    const { name, platform } = ctx.request.body;

    console.log('Request Body:', ctx.request.body);
    
    // Retornando a resposta com os dados recebidos
    ctx.send({ message: `Game: ${name}, Platform: ${platform}` });
  },
};
```

**Exemplo de corpo enviado pelo cliente:**
```json
{ "name": "Cyberpunk 2077", "platform": "PC" }
```

**Resultado esperado:**
No console será exibido:
```json
Request Body: { name: "Cyberpunk 2077", platform: "PC" }
```
A resposta será:
```json
{ "message": "Game: Cyberpunk 2077, Platform: PC" }
```

#### 3.3. Configurando a Resposta

Você pode configurar diretamente o status HTTP e o corpo da resposta no `ctx`.

**Exemplo:**

```javascript
export default {
  async notFoundExample(ctx) {
    // Configurando a resposta manualmente
    ctx.status = 404;
    ctx.body = { error: 'Not Found' };
  },
};
```

**Resultado esperado:** 
O cliente receberá:
```json
{ "error": "Not Found" }
```
E o código HTTP será 404.

### 4. Visualizando o ctx Completo

Para inspecionar todas as informações disponíveis no `ctx`, utilize um console.log simples.

**Exemplo:**

```javascript
export default {
  async inspectCtx(ctx) {
    console.log('CTX Object:', ctx);
    ctx.send('Check the server logs for the full ctx object');
  },
};
```

**Resultado esperado:** 
O console exibirá um objeto com todas as informações do `ctx`, incluindo request, response, URL, métodos HTTP, headers e muito mais.

### 5. Trabalhando com Query Parameters

Query Parameters são frequentemente usados para personalizar buscas ou filtrar resultados.

**Exemplo prático:** Buscar jogos com filtros.

**Rota no Strapi:**

```javascript
export default [
  {
    method: 'GET',
    path: '/games/filter',
    handler: 'game.filterGames',
  },
];
```

**Controller no Strapi:**

```javascript
export default {
  async filterGames(ctx) {
    const { name, os } = ctx.query;

    console.log('Query:', ctx.query);

    // Exemplo de lógica para buscar dados filtrados
    const results = [
      { id: 1, name: 'Cyberpunk 2077', os: 'Windows' },
      { id: 2, name: 'The Witcher 3', os: 'Linux' },
    ].filter(game => (!name || game.name.includes(name)) && (!os || game.os === os));

    ctx.send(results);
  },
};
```

**Requisição de exemplo:** 
`/games/filter?name=Witcher&os=Linux`

**Resposta esperada:** 
```json
[{ "id": 2, "name": "The Witcher 3", "os": "Linux" }]
```

### 6. Próximos passos

No próximo passo, você pode integrar o controller com os serviços do Strapi para acessar dados diretamente do banco de dados, tornando as consultas ainda mais dinâmicas e poderosas.

Citations:
[1] https://docs.strapi.io/dev-docs/backend-customization/requests-responses
[2] https://arthurpedroti.com.br/como-fazer-upload-download-e-exclusao-de-arquivos-com-strapi-react-e-aws-s3/
[3] https://forum.strapi.io/t/how-to-type-the-context-object-in-strapi-api-with-typescript/28935
