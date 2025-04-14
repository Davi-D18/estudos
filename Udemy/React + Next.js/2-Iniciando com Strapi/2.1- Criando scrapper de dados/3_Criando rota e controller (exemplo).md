## Rota e Controller no Strapi

### 1. O que é uma rota?

**Definição:**
Uma rota é o caminho (URL ou endpoint) que o servidor utiliza para receber e responder a requisições (como GET, POST, PUT ou DELETE). No Strapi, as rotas conectam uma URL a uma lógica específica dentro do sistema, geralmente chamada por um controller.

**Como funciona no Strapi:**
- Ao criar uma Collection Type (como "games"), o Strapi gera automaticamente rotas básicas para operações como listar, criar, atualizar e deletar.
- Para funcionalidades mais específicas, é possível criar rotas personalizadas, que definem quatro informações principais:
  - **Método:** GET, POST, PUT, DELETE (ou outro método HTTP).
  - **Caminho (path):** O URL da rota (ex.: /games/populate).
  - **Handler:** Método no controller que será chamado.
  - **Configurações opcionais:** Como autenticação e permissões.

### 2. Como criar uma rota customizada?

Para criar uma rota personalizada no Strapi, siga os passos abaixo:

1. **Acesse o diretório da API:**
   - Vá até a pasta específica da API, por exemplo: `src/api/game/routes`.

2. **Crie um novo arquivo de rotas:**
   - Nomeie o arquivo de forma descritiva, por exemplo: `populated.js`.

3. **Defina as rotas no arquivo criado:**
   As rotas devem ser exportadas como um array:

   ```javascript
   export default [
     {
       method: 'POST', // Tipo da requisição (GET, POST, etc.)
       path: '/games/populate', // Caminho da rota
       handler: 'game.populate', // Qual método do controller será chamado
     },
   ];
   ```

4. **Salve o arquivo:**
   A rota está pronta, mas será necessário criar o método correspondente no controller.

### 3. O que é um controller?

**Definição:**
Um controller é responsável por executar a lógica da aplicação quando uma rota é acessada. Ele decide o que deve ser feito com os dados da requisição e como responder ao cliente.

**Como funciona no Strapi:**
- O controller é composto por métodos (funções) que são chamados por uma rota.
- Ele pode acessar o banco de dados, manipular dados e enviar uma resposta ao cliente.

**Exemplo:**
A rota `/games/populate` pode chamar o método `populate` no controller `game` para preencher o banco de dados com informações.

### 4. Como criar um controller customizado?

Siga o passo a passo abaixo:

1. **Acesse o diretório de controllers:**
   - Vá até a pasta `src/api/game/controllers`.

2. **Edite ou crie o arquivo do controller:**
   - Se o arquivo já existir, adicione o método desejado. Caso contrário, crie um arquivo como `game.js`.

3. **Adicione o método no controller:**
   Exemplo de um método simples:

   ```javascript
   export default {
     async populate(ctx) {
       console.log('Rota executada no servidor');
       ctx.send('Finalizado no cliente');
     },
   };
   ```

4. **Salve o arquivo:**
   Agora, o controller está configurado.

### 5. Testando a rota e o controller

**Como testar:**

1. Inicie o servidor Strapi:

   ```bash
   yarn develop
   ```

2. Use uma ferramenta como Insomnia, Postman ou o terminal para enviar uma requisição:

   ```bash
   curl -X POST http://localhost:1337/games/populate
   ```

**Erro comum:** 403 Forbidden

Esse erro ocorre porque as permissões para a rota ainda não foram configuradas.

**Para resolver:**
- Acesse o painel de administração do Strapi.
- Vá em `Settings > Roles > Public`.
- Procure pela rota criada (`/games/populate`) e marque como permitida.
- Salve as alterações.

**Reenvie a requisição:** 
Após liberar a rota, envie novamente a requisição e verifique o console do servidor para ver a mensagem "Rota executada no servidor" e a resposta no cliente.

### 6. Fluxo geral de funcionamento

1. O cliente faz uma requisição para a rota, por exemplo, POST `/games/populate`.
2. A rota chama o método `populate` do controller `game`.
3. O método executa a lógica configurada:
   - Pode acessar o banco de dados.
   - Realizar operações específicas.
   - Retornar uma resposta para o cliente.
4. O cliente recebe a resposta configurada no controller.