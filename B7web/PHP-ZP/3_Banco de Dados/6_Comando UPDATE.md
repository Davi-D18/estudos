
O comando `UPDATE` é utilizado para alterar dados existentes em uma tabela no banco de dados. Ele permite atualizar valores específicos de uma ou mais colunas, baseando-se em uma condição opcional para selecionar as linhas que devem ser alteradas.

## **Estrutura Básica**
```sql
UPDATE tabela
SET coluna1 = valor1, coluna2 = valor2, ...
WHERE condicao;
```
- `tabela`: A tabela que contém os dados a serem alterados.
- `coluna1, coluna2`: As colunas que serão atualizadas.
- `valor1, valor2`: Os novos valores a serem atribuídos.
- `condicao`: (Opcional) Determina quais linhas serão atualizadas. **Sem `WHERE`, todas as linhas da tabela serão alteradas!**

---

## **1. Atualizar valores de todas as linhas**
```sql
UPDATE tabela
SET coluna = valor;
-- Atualiza todas as linhas da coluna especificada
```
### Exemplo:
```sql
UPDATE usuarios
SET status = 'ativo';
-- Define o status de todos os usuários como 'ativo'
```

---

## **2. Atualizar valores com uma condição (`WHERE`)**
```sql
UPDATE tabela
SET coluna = valor
WHERE condicao;
-- Atualiza apenas as linhas que atendem à condição
```
### Exemplo:
```sql
UPDATE usuarios
SET status = 'inativo'
WHERE ultima_atividade < '2024-01-01';
-- Define o status como 'inativo' para usuários que não acessaram desde 2024
```

---

## **3. Atualizar múltiplas colunas**
```sql
UPDATE tabela
SET coluna1 = valor1, coluna2 = valor2
WHERE condicao;
-- Atualiza várias colunas em uma única operação
```
### Exemplo:
```sql
UPDATE usuarios
SET status = 'ativo', ultima_atividade = '2024-12-01'
WHERE id = 42;
-- Define o status como 'ativo' e atualiza a última atividade do usuário com id 42
```

---

## **4. Atualizar valores incrementais**
```sql
UPDATE tabela
SET coluna = coluna + incremento
WHERE condicao;
-- Atualiza uma coluna adicionando (ou subtraindo) um valor
```
### Exemplo:
```sql
UPDATE produtos
SET estoque = estoque - 5
WHERE id = 10;
-- Reduz o estoque do produto com id 10 em 5 unidades
```

---

## **5. Atualizar com base em outra coluna**
```sql
UPDATE tabela
SET coluna1 = coluna2
WHERE condicao;
-- Copia os valores de uma coluna para outra
```
### Exemplo:
```sql
UPDATE usuarios
SET nome_exibicao = nome_real
WHERE nome_exibicao IS NULL;
-- Define o nome de exibição como o nome real, caso o primeiro esteja vazio
```

---

# **Desafios Práticos**

## **Básicos**
1. **Atualizar o status de todos os usuários para 'ativo':**
   ```sql
   UPDATE usuarios
   SET status = 'ativo';
   ```

2. **Alterar o e-mail de um usuário específico (id = 5):**
   ```sql
   UPDATE usuarios
   SET email = 'novo_email@example.com'
   WHERE id = 5;
   ```

3. **Reduzir o estoque de todos os produtos em 10 unidades:**
   ```sql
   UPDATE produtos
   SET estoque = estoque - 10;
   ```

## **Intermediários**
4. **Marcar usuários inativos que não acessam há mais de um ano:**
   ```sql
   UPDATE usuarios
   SET status = 'inativo'
   WHERE ultima_atividade < '2023-12-15';
   ```

5. **Aumentar os salários dos funcionários em 5%:**
   ```sql
   UPDATE funcionarios
   SET salario = salario * 1.05;
   ```

6. **Atualizar o estoque baseado na coluna de vendas:**
   ```sql
   UPDATE produtos
   SET estoque = estoque - vendas;
   ```

## **Avançados**
7. **Corrigir nomes em letras minúsculas para começar com maiúsculas:**
   ```sql
   UPDATE usuarios
   SET nome = CONCAT(UPPER(LEFT(nome, 1)), LOWER(SUBSTRING(nome, 2)))
   WHERE nome = LOWER(nome);
   ```

8. **Definir uma data padrão para usuários com `data_criacao` nula:**
   ```sql
   UPDATE usuarios
   SET data_criacao = '2024-01-01'
   WHERE data_criacao IS NULL;
   ```

9. **Duplicar preços de produtos com estoque abaixo de 5 unidades:**
   ```sql
   UPDATE produtos
   SET preco = preco * 2
   WHERE estoque < 5;
   ```

---

# **Resoluções e Saídas Esperadas**

1. **Atualizar o status de todos os usuários para 'ativo':**
   ```sql
   UPDATE usuarios
   SET status = 'ativo';
   -- Saída: Todas as linhas na tabela "usuarios" terão a coluna "status" alterada para 'ativo'.
   ```

2. **Alterar o e-mail de um usuário específico (id = 5):**
   ```sql
   UPDATE usuarios
   SET email = 'novo_email@example.com'
   WHERE id = 5;
   -- Saída: Apenas a linha com "id = 5" será atualizada com o novo e-mail.
   ```

3. **Reduzir o estoque de todos os produtos em 10 unidades:**
   ```sql
   UPDATE produtos
   SET estoque = estoque - 10;
   -- Saída: O estoque de todos os produtos será reduzido em 10 unidades.
   ```

---

# **Melhores Práticas**

1. **Sempre usar `WHERE` quando necessário:**
   - Evite atualizar todas as linhas da tabela acidentalmente.

2. **Testar atualizações com uma consulta `SELECT` antes:**
   - Exemplo: `SELECT * FROM tabela WHERE condicao;`
   - Isso garante que as linhas afetadas são as esperadas.

3. **Criar backups antes de operações importantes:**
   - Especialmente ao lidar com dados críticos.

4. **Evitar hardcode de valores:**
   - Utilize variáveis ou parâmetros para aumentar a flexibilidade e evitar erros.

5. **Limitar atualizações grandes:**
   - Quando possível, atualize em lotes menores para evitar bloqueios na tabela e melhorar o desempenho.

---
