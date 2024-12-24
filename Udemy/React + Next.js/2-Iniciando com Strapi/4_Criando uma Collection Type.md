# Criando uma Nova Collection Type no Strapi

O Strapi permite criar e gerenciar Collection Types, que representam tabelas ou entidades no banco de dados. Isso facilita o desenvolvimento de APIs personalizadas e a organização de conteúdo estruturado. Este guia detalha o processo de criação, configuração e uso de Collection Types no Strapi.

---

## O que é uma Collection Type?

Uma **Collection Type** é um tipo de dados no Strapi usado para armazenar entradas que compartilham a mesma estrutura. Por exemplo, uma Collection Type de "Artigos" pode ter os seguintes campos:

- **Título** (Texto)
    
- **Conteúdo** (Texto Longo)
    
- **Autor** (Relação com Usuário)
    
- **Data de Publicação** (Data)
    

Cada entrada da Collection Type seria equivalente a uma linha na tabela correspondente no banco de dados.

---

## Como Criar uma Collection Type no Strapi

### 1. Navegue até o Painel de Administração

1. Acesse o painel administrativo do seu projeto Strapi.
    
2. No menu lateral, clique em **Content-Types Builder**.
    

### 2. Comece a Criar a Collection Type

1. Clique no botão **Create new Collection Type**.
    
2. Dê um nome à sua Collection Type (ex.: "Articles").
    

### 3. Adicione Campos

1. No editor visual, clique em **Add another field**.
    
2. Escolha o tipo de campo, como:
    
    - Texto (últil para títulos e descrições).
        
    - Texto Longo (para conteúdo mais extenso).
        
    - Números (para valores numéricos).
        
    - Data (para datas e horas).
        
    - Relações (para conectar a outros tipos de dados).
        
3. Configure as propriedades do campo, como:
    
    - Nome do campo.
        
    - Opções obrigatórias (Required).
        
    - Valores padrão.
        
4. Clique em **Add field** para salvar.
    

### 4. Salve e Atualize

Depois de adicionar todos os campos desejados:

1. Clique em **Save**.
    
2. Aguarde enquanto o Strapi reinicia automaticamente para aplicar as mudanças no backend.
    

---

## Exemplos de Collection Types

### Exemplo 1: Blog Posts

**Nome:** BlogPosts  
**Campos:**

- Título (Texto)
    
- Conteúdo (Texto Longo)
    
- Categoria (Relação com "Categorias")
    
- Tags (Lista de Strings)
    
- Publicado (Booleano)
    
- Data de Publicação (Data)
    

### Exemplo 2: Produtos

**Nome:** Produtos  
**Campos:**

- Nome (Texto)
    
- Preço (Número)
    
- Estoque (Número)
    
- Descrição (Texto Longo)
    
- Imagem (Mídia)
    
- Categoria (Relação com "Categorias")
    

---

## Gerenciando Dados na Collection Type

### Adicionando Entradas

1. No painel administrativo, clique em **Collection Types**.
    
2. Escolha a Collection Type criada (ex.: BlogPosts).
    
3. Clique em **Create new entry**.
    
4. Preencha os campos com os dados desejados.
    
5. Salve a entrada.
    

### Editando ou Excluindo Entradas

1. Selecione uma entrada da lista.
    
2. Edite os valores desejados ou clique em **Delete** para removê-la.
    

---

## Dicas de Boas Práticas

1. **Nomeie Claramente**:
    
    - Escolha nomes de campos que reflitam seu propósito. (ex.: "product_name" ao invés de "name").
        
2. **Planeje Antes de Criar**:
    
    - Defina quais dados precisam ser armazenados antes de criar a Collection Type.
        
3. **Use Relações com Sabedoria**:
    
    - Evite criar relações complexas desnecessárias para manter o desempenho.
        
4. **Documente Suas Estruturas**:
    
    - Mantenha um registro de todas as Collection Types e seus campos.
        
5. **Teste o Conteúdo**:
    
    - Verifique se os dados inseridos estão sendo armazenados e exibidos corretamente.
        

---

## Explorando o Conteúdo via API

Após criar e popular uma Collection Type, os dados podem ser acessados via API REST ou GraphQL.

### Exemplo de Requisição API REST

**Endpoint GET:** `/api/articles`  
**Resposta Exemplo:**

```js
{
  "data": [
    {
      "id": 1,
      "attributes": {
        "title": "Primeiro Artigo",
        "content": "Este é o conteúdo do artigo.",
        "publishedAt": "2024-01-01T00:00:00.000Z"
      }
    }
  ]
}
```

### Exemplo de Requisição API GraphQL

**Query:**

```js
query {
  articles {
    data {
      id
      attributes {
        title
        content
      }
    }
  }
}
```

---

## Resumo

Criar uma nova Collection Type no Strapi é um processo intuitivo e poderoso para estruturar seus dados. Com uma combinação de campos flexíveis, integrações automáticas com API e ferramentas de gerenciamento fáceis de usar, o Strapi se torna uma solução ideal para projetos que demandam controle sobre o conteúdo.