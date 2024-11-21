# Scrum: Metodologia Ágil

## O que é Scrum?
- **Scrum** é um framework ágil para o desenvolvimento de projetos, especialmente software.
- Focado em **entregas rápidas** e **iterativas**.
- Baseado em ciclos curtos de trabalho, chamados de **sprints**.

## Principais Papéis no Scrum:
1. **Product Owner (PO)**:
   - Responsável por definir o que precisa ser feito.
   - Prioriza o trabalho baseado nas necessidades do cliente.
   - Cuida do **Product Backlog** (lista de funcionalidades a serem desenvolvidas).
   
2. **Scrum Master**:
   - Ajuda a equipe a seguir as práticas do Scrum.
   - Remove impedimentos e facilita o progresso do time.
   - Não é um chefe, mas um facilitador.

3. **Time de Desenvolvimento**:
   - Composto por profissionais que fazem o trabalho técnico (desenvolvedores, designers, etc.).
   - Equipe auto-organizada e multifuncional.
   - Responsável por entregar o que foi combinado na sprint.

## Ciclo de Vida do Scrum:
1. **Sprint**:
   - Período de tempo fixo (normalmente de 2 a 4 semanas).
   - Ao final de cada sprint, algo funcional e utilizável deve ser entregue.
   
2. **Sprint Planning** (Planejamento da Sprint):
   - Reunião onde o time define o que será feito durante a sprint.
   - O Product Owner prioriza os itens do **Product Backlog**.
   - O Time de Desenvolvimento seleciona o trabalho que consegue completar.

3. **Daily Scrum** (Reunião Diária):
   - Reunião curta (15 minutos) realizada todos os dias.
   - Cada membro responde 3 perguntas:
     1. O que fiz ontem?
     2. O que farei hoje?
     3. Algum impedimento?

4. **Sprint Review**:
   - Reunião ao final da sprint para mostrar o que foi desenvolvido.
   - O Product Owner valida as entregas com base nos requisitos.

5. **Sprint Retrospective**:
   - Reunião onde o time reflete sobre o que funcionou bem e o que pode melhorar.
   - Foco em melhorar o processo nas próximas sprints.

## Artefatos do Scrum:
1. **Product Backlog**:
   - Lista de todas as funcionalidades desejadas no produto.
   - Priorizada pelo Product Owner.

2. **Sprint Backlog**:
   - Subconjunto do Product Backlog que o time planeja completar na sprint atual.

3. **Incremento**:
   - Conjunto de funcionalidades que foram completadas durante a sprint.
   - Deve estar em um estado pronto para uso.

## Implementação do Scrum:
1. **Organizar o Time**: Definir os papéis (Product Owner, Scrum Master, Time de Desenvolvimento).
2. **Criar o Product Backlog**: Listar todas as funcionalidades do produto com a ajuda do Product Owner.
3. **Planejar as Sprints**: Estabelecer um ciclo de trabalho fixo (ex: sprints de 2 semanas).
4. **Realizar Reuniões Regulares**:
   - **Sprint Planning**: O que será feito na sprint.
   - **Daily Scrum**: O que está sendo feito diariamente.
   - **Sprint Review**: O que foi feito na sprint.
   - **Sprint Retrospective**: Como podemos melhorar.
5. **Entregar Incrementos Regulares**: A cada sprint, entregar algo funcional.

## Benefícios do Scrum:
- **Flexibilidade**: Fácil adaptação a mudanças de requisitos.
- **Transparência**: Comunicação constante entre o time e o cliente.
- **Entrega rápida**: Entregas pequenas e frequentes.
- **Melhoria contínua**: O time se autoavalia e melhora o processo.

## Dicas para Sucesso com Scrum:
- Mantenha as **reuniões curtas** e objetivas.
- Tenha **um backlog bem definido** e priorizado.
- Facilite a **comunicação aberta** dentro do time.
- Promova a **auto-organização** e **colaboração** no time.

---

# Como Implementar Scrum

## 1. Organize os Papéis

### Exemplo:
- Você está desenvolvendo um novo site para uma empresa.
- O time pode ser composto por:
  - **Product Owner (PO)**: Alguém que entende as necessidades da empresa e do cliente. Ele vai definir as funcionalidades principais e prioridades.
  - **Scrum Master**: Um facilitador que ajuda o time a seguir o Scrum e remove obstáculos. Pode ser um gerente de projeto ou líder técnico.
  - **Time de Desenvolvimento**: Desenvolvedores, designers, testadores, etc. Eles são responsáveis por construir o site e entregar as funcionalidades.

## 2. Crie o **Product Backlog**

O Product Backlog é a lista de todas as funcionalidades que o produto deve ter.

### Exemplo:
Para o site, o **Product Backlog** pode conter:
- Página inicial com design responsivo.
- Sistema de login de usuário.
- Seção de blog com busca.
- Carrinho de compras integrado.
- Painel de administração para gerenciar produtos.

Cada item deve ser descrito em termos simples para o time entender.

```md
**Product Backlog**:
1. Página inicial com design responsivo.
2. Sistema de login de usuário.
3. Seção de blog com busca.
4. Carrinho de compras integrado.
5. Painel de administração para gerenciar produtos.
```

## 3. Priorize o Backlog

O Product Owner vai definir a ordem de prioridade das funcionalidades.

### Exemplo:

- O sistema de login de usuário pode ser prioridade alta, já que os usuários precisam se registrar para acessar certas áreas.
- A seção de blog pode ser prioridade média, pois não é essencial para o primeiro lançamento.

```md
**Product Backlog (Prioridade)**: 
1. Sistema de login de usuário (Alta). 
2. Página inicial com design responsivo (Alta). 
3. Carrinho de compras integrado (Média). 
4. Painel de administração para gerenciar produtos (Média). 
5. Seção de blog com busca (Baixa).
```

### Sprint Backlog (Sprint 1):
1. Sistema de login de usuário.
2. Página inicial com design responsivo.

O time pega esses itens do **Product Backlog** e move para o **Sprint Backlog**.

## 5. Daily Scrum (Reunião Diária)

Todos os dias, o time realiza uma reunião curta (15 minutos), onde cada membro responde:

1. O que fiz ontem?
2. O que farei hoje?
3. Algum impedimento?

### Exemplo de reunião:

- Desenvolvedor 1: "Ontem, configurei a autenticação do login. Hoje, vou implementar a verificação de e-mail. Sem impedimentos."
- Designer: "Ontem, finalizei o design da página inicial. Hoje, vou ajustar o layout responsivo para mobile."
- Desenvolvedor 2: "Estou tendo problemas com a integração da API de login."

O **Scrum Master** resolve o problema para o Desenvolvedor 2.

## 6. Sprint Review (Revisão da Sprint)

No final da sprint (ex: 2 semanas), o time mostra o que foi feito para o Product Owner.

### Exemplo:

- O time apresenta o sistema de login funcionando e a página inicial com design responsivo.
- O Product Owner testa e valida o trabalho. Se algo não estiver funcionando como esperado, pode ser ajustado na próxima sprint.

## 7. Sprint Retrospective (Retrospectiva da Sprint)
Depois da sprint, o time faz uma reunião para discutir o que deu certo e o que pode melhorar.
### Exemplo:

- O time percebe que subestimou o tempo necessário para o sistema de login.
- Decidem melhorar o planejamento da próxima sprint.

## 8. Comece uma Nova Sprint

Após a retrospectiva, o time começa uma nova sprint, repetindo o ciclo.
### Exemplo:

Na **Sprint 2**, o time pode escolher trabalhar no **Carrinho de Compras** e no **Painel de Administração**.
```md
	Sprint Backlog (Sprint 2):
	1. Carrinho de compras integrado.
	2. Painel de administração para gerenciar produtos.
```

## Implementando Scrum na Prática

### Passos para Implementação:

1. **Formar o time**: Defina os papéis de Product Owner, Scrum Master e Time de Desenvolvimento.
2. **Criar o Product Backlog**: Liste todas as funcionalidades desejadas no projeto.
3. **Planejar a primeira Sprint**: Priorize o que é mais importante e escolha os itens para a primeira sprint.
4. **Realizar reuniões diárias**: Mantenha as Daily Scrums para acompanhamento do progresso.
5. **Mostrar resultados**: Ao final da sprint, apresente as entregas na Sprint Review.
6. **Refletir e melhorar**: Na Sprint Retrospective, discuta melhorias para o próximo ciclo.
7. **Repetir o processo**: Continue planejando e executando sprints até completar o projeto.

## Ferramentas para Implementar Scrum:

- **Trello**: Organize seu Product Backlog e Sprint Backlog em quadros.
- **Jira**: Ferramenta mais robusta para gerenciar projetos Scrum.
- **GitHub Projects**: Útil para equipes que já usam GitHub, permite criar quadros e acompanhar tarefas.
- **Slack**: Para comunicação rápida entre o time, especialmente para reuniões diárias.