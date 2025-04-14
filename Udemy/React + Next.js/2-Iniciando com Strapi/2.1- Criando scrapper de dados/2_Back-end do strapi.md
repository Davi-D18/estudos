### O que é o Back-End do Strapi?

- O back-end do Strapi é um servidor HTTP que lida com requisições para criar, recuperar, atualizar ou deletar dados.
    
- Ele utiliza o **Koa.js**, um framework JavaScript eficiente e modular.
    
- Funciona em conjunto com um banco de dados, gerenciando o conteúdo do seu site ou aplicativo.
    

---

### Fluxo da Requisição no Back-End do Strapi

1. **Requisição**:
    
    - Uma requisição é enviada ao servidor HTTP do Strapi (REST ou GraphQL).
        
2. **Middlewares Globais**:
    
    - São as primeiras camadas que processam a requisição.
        
    - Podem validar, alterar ou bloquear o acesso antes de seguir para as rotas.
        
3. **Rota**:
    
    - Aponta para um controlador. Cada tipo de conteúdo criado gera automaticamente uma rota (ex.: `/articles`, `/users`).
        
    - Rotas personalizadas também podem ser adicionadas.
        
4. **Políticas e Middlewares de Rota**:
    
    - Políticas verificam permissões (ex.: um usuário pode acessar essa rota?).
        
    - Middlewares de rota podem modificar ou validar dados antes de chegarem ao controlador.
        
5. **Controladores**:
    
    - São funções que executam a lógica principal quando uma rota é acessada.
        
    - Ex.: “Buscar todos os artigos do banco de dados”.
        
6. **Serviços (Opcional)**:
    
    - Códigos reutilizáveis que ajudam os controladores a realizar tarefas específicas.
        
7. **Banco de Dados**:
    
    - Interação com os dados ocorre através de **modelos** e do **Mecanismo de Consulta (Query Engine)**.
        
    - Hooks de ciclo de vida e middlewares podem ser usados para manipular os dados antes ou depois da consulta.
        
8. **Resposta**:
    
    - Dados processados pelo back-end são enviados de volta para o cliente.
        
    - Middlewares podem alterar a resposta antes de ser enviada.
        

---

### Personalização do Back-End

#### 1. Adicionando ou Modificando Rotas:

- No diretório `src/api/<content-type>/routes`, você pode:
    
    - Alterar rotas geradas automaticamente.
        
    - Adicionar novas rotas manualmente.
        

Exemplo de uma rota personalizada:

```js
module.exports = {
  routes: [
    {
      method: 'GET',
      path: '/custom-route',
      handler: 'custom-controller.customAction',
      config: {
        policies: ['is-authenticated'],
      },
    },
  ],
};
```

#### 2. Criando Controladores Personalizados:

- No diretório `src/api/<content-type>/controllers`, você pode adicionar lógica customizada.
    

Exemplo de controlador:

```js
module.exports = {
  async customAction(ctx) {
    const data = await strapi.db.query('api::article.article').findMany();
    ctx.body = data;
  },
};
```

#### 3. Adicionando Serviços Personalizados:

- Serviços ficam no diretório `src/api/<content-type>/services`.
    
- Eles ajudam a separar a lógica de negócios do controlador.
    

Exemplo de serviço:

```js
module.exports = {
  async fetchArticles() {
    return await strapi.db.query('api::article.article').findMany();
  },
};
```

#### 4. Utilizando Hooks e Middlewares:

- **Hooks**: Executam tarefas antes ou depois de ações no banco de dados.
    
    - Configuração: `src/api/<content-type>/content-types/<content-name>/lifecycles.js`.
        

Exemplo de um hook:

```js
module.exports = {
  async beforeCreate(event) {
    const { data } = event.params;
    data.createdAt = new Date();
  },
};
```

- **Middlewares**: Interceptam requisições ou respostas.
    
    - Configuração: `config/middlewares.js`.
        

Exemplo de middleware:

```js
module.exports = (config, { strapi }) => {
  return async (ctx, next) => {
    console.log('Middleware executado antes da rota');
    await next();
  };
};
```

---

### Benefícios da Personalização no Strapi

1. **Flexibilidade**: Você pode criar rotas, controladores e serviços que atendem às suas necessidades.
    
2. **Modularidade**: Reutilize código em diferentes partes do sistema.
    
3. **Escalabilidade**: Adapte o Strapi para atender a aplicações mais complexas.
    
4. **Segurança**: Adicione políticas e middlewares para proteger rotas e dados.
    

### Boas Práticas:

- Documente as personalizações feitas.
    
- Teste exaustivamente rotas e controladores.
    
- Evite manipular o banco diretamente; use os serviços e o mecanismo de consulta.
    
- Atualize o Strapi regularmente para aproveitar correções e melhorias.