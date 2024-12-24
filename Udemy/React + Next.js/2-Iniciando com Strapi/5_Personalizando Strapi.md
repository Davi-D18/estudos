## Alterando a Aparência Padrão do Strapi

A interface administrativa do Strapi pode ser personalizada para atender às necessidades específicas do projeto.

### Personalização de Tema (Admin UI)

O Strapi permite alterar o tema do painel administrativo para ajustar cores, logotipo e muito mais.

1. **Adicione um Arquivo de Extensão**:
    
    - Crie o diretório `src/admin` no seu projeto.
        
    - Dentro dele, crie um arquivo `src/admin/app.js`.
        
2. **Modifique o Tema**:
    
    - Edite o arquivo `app.js` para incluir um tema customizado.
        

**Exemplo de Configuração de Tema:**

```
export default {
  config: {
    theme: {
      colors: {
        primary100: '#E3F2FD',
        primary500: '#2196F3',
        primary600: '#1E88E5',
        primary700: '#1976D2',
      },
    },
    locales: [
      'en', 'fr', 'es',
    ],
    logo: './extensions/my-custom-logo.png',
  },
  bootstrap(app) {
    console.log('Admin panel customizado carregado!');
  },
};
```

### Alterando o Logotipo

- Adicione a imagem do logotipo na pasta `extensions`.
    
- Referencie o caminho da imagem no arquivo `app.js`, como mostrado acima.
    

### Mudando Idiomas do Painel Administrativo

Adicione os idiomas desejados no array `locales`. O idioma padrão pode ser configurado no arquivo de configuração geral do Strapi.

---

## Personalização de URLs

Você pode modificar as URLs padrões da API e da interface administrativa do Strapi para se adequarem às necessidades do projeto.

### Mudança da URL Administrativa

1. **Localize o arquivo de configuração:**
    
    - O arquivo está em `./config/server.js`.
        
2. **Edite o arquivo:**
    
    - Altere a propriedade `admin.url` para o caminho desejado.
        

**Exemplo:**

```
module.exports = ({ env }) => ({
  admin: {
    url: '/dashboard',
  },
});
```

### Alterando URLs da API

- Modifique o prefixo da API utilizando o arquivo `server.js`.
    

**Exemplo:**

```
module.exports = ({ env }) => ({
  routes: {
    prefix: '/custom-api',
  },
});
```

Com isso, todas as rotas da API começarão com `/custom-api`.

---

## Extensões de Plugins

O Strapi permite personalizar o comportamento de plugins integrados ou criar novas funcionalidades.

### Exemplo: Customização do Plugin de Autenticação

1. **Adicione uma extensão:**
    
    - Crie a pasta `src/extensions/users-permissions/`.
        
2. **Modifique o Comportamento:**
    
    - Adicione ou edite os arquivos de configuração do plugin.
        

**Exemplo:**

```
module.exports = {
  settings: {
    jwt: {
      expiresIn: '7d',
    },
  },
};
```

### Criando um Plugin Personalizado

1. **Gerar Plugin:**
    
    - Use o comando CLI:
        
    
    ```
    npx strapi generate plugin my-plugin
    ```
    
2. **Estrutura do Plugin:**
    
    - A estrutura do plugin será criada na pasta `src/plugins/my-plugin`.
        
3. **Registrar o Plugin:**
    
    - Certifique-se de que o plugin está registrado no arquivo principal de configuração.
        

---

## Personalização de Middleware

Os middlewares permitem interceptar e modificar requisições ou respostas da API. Você pode adicionar middlewares customizados no Strapi.

1. **Adicione o Middleware:**
    
    - Crie ou edite o arquivo em `./config/middleware.js`.
        

**Exemplo de Middleware Customizado:**

```
module.exports = [
  {
    name: 'my-custom-middleware',
    config: {
      enabled: true,
      resolve: './src/middlewares/my-middleware.js',
    },
  },
];
```

2. **Implemente o Middleware:**
    
    - Crie o arquivo `./src/middlewares/my-middleware.js` com o código desejado.
        

**Exemplo:**

```
module.exports = async (ctx, next) => {
  console.log('Request interceptada:', ctx.request.url);
  await next();
};
```

---

## Melhores Práticas para Customização

1. **Mantenha a Estrutura Limpa:**
    
    - Separe suas customizações em diretórios adequados como `src/extensions` e `src/admin`.
        
2. **Documente suas Mudanças:**
    
    - Registre todas as alterações feitas para facilitar a manutenção.
        
3. **Evite Alterar o Core do Strapi:**
    
    - Sempre use as extensões para customizar, evitando alterar arquivos nativos do framework.
        
4. **Teste as Customizações:**
    
    - Teste exaustivamente todas as customizações para garantir que funcionam corretamente em todos os cenários.