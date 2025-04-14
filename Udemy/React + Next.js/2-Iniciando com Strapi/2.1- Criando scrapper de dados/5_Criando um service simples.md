## O que é um Service no Strapi?

Um **Service** no Strapi é uma função que contém lógica reutilizável em vários locais do seu código. Eles ajudam a manter o código limpo e **DRY** (Don't Repeat Yourself), evitando duplicação ao permitir que você centralize a lógica.

### Principais Vantagens dos Services:
- **Reutilização:** Permite encapsular lógicas que serão chamadas em múltiplos pontos do sistema.
- **Manutenção:** Lógica de negócio isolada em um único local facilita ajustes futuros.
- **Testabilidade:** Com serviços centralizados, fica mais fácil testá-los separadamente.
- **Modularidade:** Cada Service pode ser especializado em um contexto específico.

## Criando um Service Simples no Strapi

Vamos construir um exemplo prático para consolidar o conceito.

### 1. Estrutura de Arquivos

No Strapi, cada Collection Type ou Single Type pode ter seus próprios Services. Os arquivos de Service ficam em:

```javascript
src/api/<nome-da-entidade>/services/<nome-do-service>.js
```

Por exemplo, se você tem uma coleção chamada `game`, o arquivo de serviço dela será:

```bash
src/api/game/services/game.js
```

### 2. Exemplo de Lógica Simples

A ideia aqui será criar um método para buscar uma categoria com base no nome recebido como parâmetro.

#### Etapa 1: Criar o Método no Service

No arquivo `game.js`, vamos implementar um método chamado `populate`, que filtra categorias com base no nome recebido:

```javascript
'use strict';

module.exports = {
  async populate(params) {
    // Log para entender os parâmetros recebidos
    console.log('Parâmetros recebidos:', params);

    // Acessa o Service de categorias dentro do próprio Service
    const categories = await strapi.service('api::category.category').find({
      filters: {
        name: params.category, // Filtra categorias pelo nome recebido
      },
    });

    // Retorna as categorias encontradas ou vazio
    return categories?.results || [];
  },
};
```

Aqui:
- O método `populate` é assíncrono porque utiliza a função `find` para buscar dados.
- Ele utiliza o Service da entidade `category` (ou seja, `api::category.category`) para buscar os dados com base nos filtros passados.
- O retorno será uma lista de categorias que correspondem ao filtro ou um array vazio se nenhuma categoria for encontrada.

#### Etapa 2: Chamar o Service no Controller

Agora que o serviço está pronto, precisamos chamá-lo no Controller. No Strapi, os Controllers são responsáveis por receber as requisições e direcioná-las.

No arquivo do Controller `game.js`:

```javascript
'use strict';

module.exports = {
  async populate(ctx) {
    try {
      // Pega os parâmetros da requisição
      const params = ctx.query;

      // Chama o Service e obtém os dados
      const categories = await strapi.service('api::game.game').populate(params);

      // Retorna as categorias encontradas
      ctx.send({ categories });
    } catch (err) {
      ctx.badRequest('Ocorreu um erro ao popular os dados.', { error: err.message });
    }
  },
};
```

Aqui:
- `ctx.query`: Captura os parâmetros enviados na URL, como `?category=Action`.
- O Service `populate` do Game é chamado, passando os parâmetros recebidos.
- O resultado é enviado de volta na resposta HTTP.

#### Etapa 3: Testar no Navegador ou via cURL

Com o Service e Controller configurados, você pode testá-lo enviando uma requisição para o endpoint associado. Por exemplo:

```bash
curl http://localhost:1337/api/games/populate?category=Action
```

Ou simplesmente acesse no navegador:

```bash
http://localhost:1337/api/games/populate?category=Action
```

Se a categoria Action existir, ela será retornada; caso contrário, o resultado será vazio.

### Aprofundando no Funcionamento

#### Usando Métodos do Core do Strapi

O Strapi fornece métodos prontos para as operações principais, como:
- **find:** Busca múltiplos registros.
- **findOne:** Busca um único registro.
- **create:** Cria um novo registro.
- **update:** Atualiza um registro.
- **delete:** Remove registros.

Você pode usá-los diretamente nos Services ou estendê-los para incluir lógica adicional.

**Exemplo de estender o método find:**

```javascript
async find(params) {
  const results = await super.find(params); // Chama o método original
  // Adiciona lógica personalizada, se necessário
  return results.map(item => ({
    ...item,
    customField: 'Adicionado no Serviço',
  }));
}
```

#### Filtros e Relações

Os filtros permitem buscar dados baseados em critérios. Além disso, você pode incluir relações para carregar dados relacionados:

```javascript
await strapi.service('api::category.category').find({
  filters: { name: 'Action' },
  populate: ['relatedField'], // Carrega o campo relacionado
});
```

#### Usando Serviços dentro de Serviços

É possível criar uma cadeia de dependências usando Services dentro de outros Services. Isso permite lógica mais complexa e reutilização ainda maior.

### Boas Práticas com Services

- **Mantenha a Simplicidade:** Cada Service deve ter uma responsabilidade clara e bem definida.
- **Centralize a Lógica de Negócio:** Qualquer lógica complexa ou que precise ser usada em múltiplos lugares deve ser movida para um Service.
- **Documente Bem:** Inclua comentários explicativos para facilitar a manutenção.
- **Teste os Services:** Services podem ser testados isoladamente, aumentando a confiança no código.

Citations:
[1] https://www.iugu.com/blog/criar-api-com-strapi
[2] https://inovatechy.com/strapi-o-cms-headless-que-sua-empresa-precisa/
[3] https://www.treinaweb.com.br/blog/criando-apis-com-o-strapi-io
[4] https://docs.strapi.io/dev-docs/backend-customization/services
[5] https://www.linkedin.com/pulse/strapi-potente-ferramenta-para-gest%C3%A3o-de-conte%C3%BAdo-matheus-ux7tf