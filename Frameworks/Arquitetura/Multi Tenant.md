## O que é?

Multi-tenant é uma abordagem de arquitetura de software onde uma única instância de uma aplicação serve múltiplos clientes (tenants). Cada tenant é isolado dos outros, embora compartilhem a mesma aplicação.

Cada tenant é uma entidade distinta, como uma empresa ou organização, e pode ter seus próprios dados e configurações.

## O que é um tenant?

É uma entidade ou ator do sistema, que dependendo da situação, pode ser, por exemplo:

- Um usuário
- Uma empresa
- Um grupo

Exemplo: [Link](https://whimsical.com/multi-tenant-HB42F6FVyV5vXBWv1HDUJU)

## Tipos diferentes da arquitetura Multi Tenant

1. Isolamento de Banco de Dados
    
    - Múltiplos tenants compartilham a mesma instância da aplicação, mas possuem bancos de dados separados
2. Isolamento de schema
    
    - Múltiplos tenants compartilham a mesma instância da aplicação e o mesmo banco de dados, mas com esquemas diferentes
3. Isolamento de Tabela (ou compartilhado)
    
    - Múltiplos tenants compartilham a mesma instância da aplicação e o mesmo banco de dados, mas com tabelas diferentes

## Dicas

Isolamento de tabela (ou compartilhado), na maioria das vezes resolve o problema, além de ser o mais fácil de implementar. **Se resolve apenas com modelagem e permissões!**

Se for usar Django, ele já traz uma séria de facilidades e coisas prontas, como:

- Estrutura completa de usuários
- Estrutura completa de permissões
- Opção de Mixins personalizados de permissões
- Fácil modelagem e reaproveitamento