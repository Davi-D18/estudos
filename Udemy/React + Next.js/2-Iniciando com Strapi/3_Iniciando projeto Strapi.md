## Como Iniciar um Projeto Strapi

### 1. Instalação

- **Via Yarn**:
    
    ```
    yarn create strapi
    ```
    
- **Via NPX**:
    
    ```
    npx create-strapi@latest
    ```
    

### 2. Configuração do Banco de Dados

- Escolha entre SQLite (padrão para desenvolvimento), PostgreSQL, MySQL ou MariaDB durante a instalação.
    

### 3. Inicialização do Servidor

- Navegue até o diretório do projeto:
    
    ```
    cd nome-do-projeto
    ```
    
- Inicie o servidor:
    
    ```
    yarn develop
    ```
    
- Acesse o painel administrativo em `http://localhost:1337/admin`.
    

---

## Configurações Importantes

### 1. Conexões de Banco de Dados

- Configuradas no arquivo `config/database.js`.
    
- Exemplos:
    
    ```js
    module.exports = {
      connection: {
        client: 'postgres',
        connection: {
          host: 'localhost',
          port: 5432,
          database: 'meu_banco',
          user: 'meu_usuario',
          password: 'minha_senha',
        },
      },
    };
    ```
    

### 2. Configuração do Servidor

- Ajustes em `config/server.js`:
    
    ```js
    module.exports = {
      host: 'localhost',
      port: 1337,
      app: {
        keys: ['minha-chave-secreta'],
      },
    };
    ```
    

### 3. Middlewares

- Configurados em `config/middlewares.js` para funções como CORS e autenticação.
    

### 4. Plugins

- Arquitetura extensível para adicionar funcionalidades, como suporte a GraphQL e internacionalização (i18n).
    

---

## Desenvolvimento com Strapi

### Tipos de Conteúdo

- Criados pelo Content-Type Builder no painel administrativo ou via código em `/api`.
    

### Controllers e Services

- Controllers: Localizados em `/src/api/[tipo-de-conteudo]/controllers`.
    
- Services: Localizados em `/src/api/[tipo-de-conteudo]/services`.
    

### Rotas Personalizadas

- Definidas em `/src/api/[tipo-de-conteudo]/routes`.
    
- Exemplo:
    
    ```js
    module.exports = {
      routes: [
        {
          method: 'GET',
          path: '/custom-route',
          handler: 'custom-controller.customAction',
        },
      ],
    };
    ```
    

---

## Recursos Adicionais

- **Internacionalização (i18n)**: Gerencie conteúdo em múltiplos idiomas.
    
- **Media Library**: Biblioteca integrada para gerenciar arquivos de mídia.
    
- **Autenticação e Autorização**: Sistema robusto de gestão de usuários, roles e permissões.
    
- **APIs REST e GraphQL**: Suporte nativo para ambos os formatos.