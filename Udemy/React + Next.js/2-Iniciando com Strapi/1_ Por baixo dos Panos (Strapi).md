## O que é o Strapi?

O **Strapi** é um CMS (Content Management System) de código aberto baseado em Node.js. Ele é uma ferramenta poderosa para criar APIs e gerenciar conteúdo de maneira eficiente, com suporte à personalização e à integração com diversos front-ends.

### Principais Características:

- **Headless CMS**: O Strapi é "headless", o que significa que ele fornece apenas uma API para gerenciar e acessar conteúdo. O front-end pode ser construído com qualquer tecnologia.
    
- **Personalização Completa**: Permite modificar modelos, endpoints e o painel administrativo.
    
- **Baseado em Node.js**: Leve, rápido e fácil de integrar com outras ferramentas.
    
- **Suporte a Plugins**: Permite extensão da funcionalidade através de plugins.
    
- **Administração via Interface Gráfica**: Interface intuitiva para gerenciar coleções de dados.
    

---

## Como Funciona o Strapi por De Baixo dos Panos

### Estrutura de Arquivos

O Strapi segue uma arquitetura modular e organizada:

1. `**api**`: Contém as coleções e os controladores criados para a aplicação.
    
2. `**config**`: Configuração do projeto, como conexões com banco de dados e middleware.
    
3. `**extensions**`: Personalizações de funcionalidades internas do Strapi.
    
4. `**plugins**`: Diretório para instalar e configurar plugins.
    
5. `**public**`: Arquivos estáticos servidos pelo Strapi.
    
6. `**src**`: Código-fonte principal do projeto.
    

### Componentes Principais

- **Modelos e Coleções**:
    
    - Os modelos definem a estrutura dos dados, enquanto as coleções são os dados em si armazenados no banco.
        
- **Controladores**:
    
    - Funções que contêm a lógica de negócio e respondem às solicitações de API.
        
- **Serviços**:
    
    - Camada de abstração para facilitar o reuso da lógica de negócio em diferentes partes da aplicação.
        
- **Middlewares**:
    
    - Interceptam requisições e respostas para adicionar funcionalidades, como autenticação.
        
- **Banco de Dados**:
    
    - O Strapi é compatível com bancos SQL (MySQL, PostgreSQL, SQLite) e NoSQL (MongoDB).
        

---

## Como Usar o Strapi

### 1. Instalação

O Strapi pode ser instalado globalmente ou no projeto local:

```
npx create-strapi-app my-project --quickstart
```

Este comando:

- Instala o Strapi.
    
- Configura o SQLite como banco de dados padrão (pode ser alterado).
    
- Inicia o servidor.
    

### 2. Criar Coleções de Dados

Uma coleção é um conjunto de dados com uma estrutura definida. Para criar:

1. Acesse o painel administrativo.
    
2. Clique em **Content-Type Builder**.
    
3. Adicione campos à sua coleção (ex.: texto, número, relações).
    

**Exemplo de Modelo:**

```json
{
  "kind": "collectionType",
  "collectionName": "articles",
  "info": {
    "name": "Article"
  },
  "attributes": {
    "title": {
      "type": "string",
      "required": true
    },
    "content": {
      "type": "text"
    },
    "author": {
      "model": "user",
      "via": "articles"
    }
  }
}
```

### 3. Configurar o Banco de Dados

Altere o banco de dados no arquivo `config/database.js`.

**Exemplo com PostgreSQL:**

```
module.exports = ({ env }) => ({
  connection: {
    client: 'postgres',
    connection: {
      host: env('DATABASE_HOST', 'localhost'),
      port: env.int('DATABASE_PORT', 5432),
      database: env('DATABASE_NAME', 'my_database'),
      user: env('DATABASE_USER', 'my_user'),
      password: env('DATABASE_PASSWORD', 'my_password'),
    },
  },
});
```

### 4. Consultar a API

Uma vez que as coleções estão configuradas, o Strapi gera endpoints automáticos.

**Exemplo:**

- `GET /articles`: Retorna todos os artigos.
    
- `POST /articles`: Cria um novo artigo (autenticação necessária).
    

Use ferramentas como Postman para testar os endpoints.

---

## Personalização do Strapi

### Criar um Controlador Personalizado

**Exemplo:** Adicionar validação ao criar um artigo.

1. Crie o arquivo `api/article/controllers/article.js`:
    
    ```
    module.exports = {
      async create(ctx) {
        const { title, content } = ctx.request.body;
    
        if (!title) {
          return ctx.badRequest('O título é obrigatório');
        }
    
        const article = await strapi.services.article.create({ title, content });
        return article;
      },
    };
    ```
    

### Adicionar Plugins

O Strapi possui plugins que expandem funcionalidades:

- **GraphQL**:
    
    ```
    npm install @strapi/plugin-graphql
    ```
    
    - Acesse o painel administrativo e habilite o plugin.
        
- **Upload**: Para gerenciar uploads de arquivos.
    

---

## Contexto de Boilerplate com o Strapi

Um **boilerplate** é um projeto base com configurações iniciais pré-definidas. Com o Strapi, você pode criar um boilerplate para acelerar futuros projetos.

### Como Funciona

1. **Crie um Projeto Base**:
    
    - Configure coleções comuns, plugins e autenticação.
        
2. **Exporte o Projeto**:
    
    - Use o comando `git` para versionar o projeto inicial.
        
3. **Reutilize**:
    
    - Clone o repositório em novos projetos e ajuste conforme necessário.
        

### Exemplo de Uso

Imagine um projeto que sempre precisa de "Usuários", "Artigos" e "Categorias":

- Configure essas coleções no projeto base.
    
- Adicione plugins como GraphQL e Upload.
    
- Crie relações pré-definidas, como "Artigos pertencem a uma Categoria".
    

---

## Melhores Práticas com Strapi

1. **Planeje o Modelo de Dados**:
    
    - Estruture as coleções antes de criar o projeto para evitar retrabalho.
        
2. **Versione o Projeto**:
    
    - Use Git para acompanhar mudanças em coleções e configurações.
        
3. **Proteja os Endpoints**:
    
    - Configure permissões para evitar acessos indesejados.
        
4. **Documente a API**:
    
    - Utilize plugins ou ferramentas externas para documentação clara.
        
5. **Teste Antes de Implantar**:
    
    - Use ferramentas como Postman para garantir que os endpoints estão funcionando corretamente.
        
6. **Atualizações e Backups**:
    
    - Atualize regularmente para aproveitar novos recursos e corrijir vulnerabilidades.
        
    - Realize backups periódicos do banco de dados e arquivos.
        

---

## Resumo

O Strapi é uma ferramenta flexível e poderosa para construir APIs e gerenciar conteúdo. Sua arquitetura modular e personalizável o torna ideal para aplicações modernas. Com a abordagem headless, você tem liberdade para usar qualquer tecnologia de front-end, garantindo um desenvolvimento rápido e eficiente.