# Anotações sobre o comando `SELECT`

O comando `SELECT` é utilizado para recuperar dados de uma ou mais tabelas em um banco de dados. Ele permite selecionar colunas específicas, aplicar filtros, ordenar resultados e realizar diversas operações para manipular os dados retornados.

## **Estrutura Básica**
```sql
SELECT coluna1, coluna2, ...
FROM tabela
WHERE condicao;
```
- `coluna1, coluna2`: As colunas que você deseja buscar.
- `tabela`: A tabela de onde os dados serão extraídos.
- `condicao`: (Opcional) Uma condição para filtrar os resultados.

---

## **1. Selecionar todas as colunas**
```sql
SELECT * FROM tabela;
-- Retorna todas as colunas e linhas da tabela
```
### Exemplo:
```sql
SELECT * FROM usuarios;
-- Retorna todos os dados da tabela "usuarios"
```

---

## **2. Selecionar colunas específicas**
```sql
SELECT coluna1, coluna2 FROM tabela;
-- Retorna apenas as colunas especificadas
```
### Exemplo:
```sql
SELECT nome, email FROM usuarios;
-- Retorna as colunas "nome" e "email" de todos os usuários
```

---

## **3. Filtrar resultados com `WHERE`**

### **3.1 Filtrar por igualdade**
```sql
SELECT * FROM tabela WHERE coluna = 'valor';
-- Retorna apenas as linhas onde a coluna especificada é igual ao valor fornecido
```
### Exemplo:
```sql
SELECT * FROM usuarios WHERE nome = 'João';
-- Retorna os usuários cujo nome é "João"
```

### **3.2 Filtrar por padrão usando `LIKE`**
```sql
SELECT * FROM tabela WHERE coluna LIKE 'padrão';
-- Retorna as linhas que correspondem ao padrão especificado
```
- `%`: Substitui qualquer sequência de caracteres.
- `_`: Substitui um único caractere.

### Exemplos:
```sql
SELECT * FROM usuarios WHERE nome LIKE 'A%';
-- Retorna os usuários cujo nome começa com "A"

SELECT * FROM usuarios WHERE email LIKE '%@gmail.com';
-- Retorna os usuários com e-mails do domínio "@gmail.com"
```

---

## **4. Ordenar resultados com `ORDER BY`**

### **4.1 Ordem crescente (padrão)**
```sql
SELECT * FROM tabela ORDER BY coluna ASC;
-- Retorna os dados ordenados em ordem crescente com base na coluna especificada
```
### Exemplo:
```sql
SELECT * FROM usuarios ORDER BY nome ASC;
-- Retorna todos os usuários em ordem alfabética pelo nome
```

### **4.2 Ordem decrescente**
```sql
SELECT * FROM tabela ORDER BY coluna DESC;
-- Retorna os dados ordenados em ordem decrescente
```
### Exemplo:
```sql
SELECT * FROM usuarios ORDER BY nome DESC;
-- Retorna todos os usuários em ordem alfabética inversa pelo nome
```

---

## **5. Contar registros com `COUNT`**
```sql
SELECT COUNT(*) FROM tabela;
-- Retorna o número total de registros na tabela
```
### Exemplo:
```sql
SELECT COUNT(*) FROM usuarios;
-- Retorna a quantidade total de usuários
```

---

## **6. Evitar duplicatas com `DISTINCT`**
```sql
SELECT DISTINCT coluna FROM tabela;
-- Retorna apenas valores únicos da coluna especificada
```
### Exemplo:
```sql
SELECT DISTINCT email FROM usuarios;
-- Retorna todos os e-mails únicos da tabela "usuarios"
```

---

## **7. Usar alias (apelidos) com `AS`**
```sql
SELECT coluna AS apelido FROM tabela;
-- Renomeia uma coluna no resultado
```
### Exemplo:
```sql
SELECT nome AS "Nome do Usuário", email AS "E-mail" FROM usuarios;
-- Renomeia as colunas "nome" e "email" para "Nome do Usuário" e "E-mail", respectivamente
```

---

## **8. Limitar resultados com `LIMIT`**
```sql
SELECT * FROM tabela LIMIT n;
-- Retorna apenas as "n" primeiras linhas
```
### Exemplo:
```sql
SELECT * FROM usuarios LIMIT 5;
-- Retorna os 5 primeiros usuários
```

---

# **Desafios Práticos**

## **Básicos**
1. **Listar todos os usuários da tabela:**
   ```sql
   SELECT * FROM usuarios;
   -- Retorna todos os dados da tabela "usuarios"
   ```

2. **Mostrar apenas os nomes e os e-mails:**
   ```sql
   SELECT nome, email FROM usuarios;
   -- Retorna as colunas "nome" e "email"
   ```

3. **Filtrar por nomes que começam com a letra 'A':**
   ```sql
   SELECT * FROM usuarios WHERE nome LIKE 'A%';
   -- Retorna os usuários cujo nome começa com "A"
   ```

4. **Encontrar usuários com e-mails do domínio `example.com`:**
   ```sql
   SELECT * FROM usuarios WHERE email LIKE '%@example.com';
   -- Retorna os usuários com e-mails terminando em "@example.com"
   ```

## **Intermediários**
5. **Ordenar usuários por nome em ordem alfabética:**
   ```sql
   SELECT * FROM usuarios ORDER BY nome ASC;
   -- Retorna os dados ordenados por nome em ordem crescente
   ```

6. **Ordenar por nome em ordem decrescente:**
   ```sql
   SELECT * FROM usuarios ORDER BY nome DESC;
   -- Retorna os dados ordenados por nome em ordem decrescente
   ```

7. **Selecionar usuários com a senha 'senha123':**
   ```sql
   SELECT * FROM usuarios WHERE senha = 'senha123';
   -- Retorna os usuários cuja senha é "senha123"
   ```

8. **Procurar usuários cujos nomes contenham a palavra 'Silva':**
   ```sql
   SELECT * FROM usuarios WHERE nome LIKE '%Silva%';
   -- Retorna os usuários cujo nome contém "Silva"
   ```

## **Avançados**
9. **Contar o número total de usuários na tabela:**
   ```sql
   SELECT COUNT(*) AS total_usuarios FROM usuarios;
   -- Retorna a quantidade total de usuários
   ```

10. **Encontrar usuários com senhas que terminam em '303':**
    ```sql
    SELECT * FROM usuarios WHERE senha LIKE '%303';
    -- Retorna os usuários cuja senha termina com "303"
    ```

11. **Filtrar e-mails únicos (sem duplicatas):**
    ```sql
    SELECT DISTINCT email FROM usuarios;
    -- Retorna os e-mails únicos
    ```

12. **Procurar por nomes que têm exatamente 5 letras:**
    ```sql
    SELECT * FROM usuarios WHERE nome LIKE '_____';
    -- Retorna os usuários com nomes de exatamente 5 letras
    ```

13. **Contar usuários com senhas que começam com 'abc':**
    ```sql
    SELECT COUNT(*) FROM usuarios WHERE senha LIKE 'abc%';
    -- Retorna a quantidade de usuários cuja senha começa com "abc"
    ```

14. **Listar os 10 primeiros usuários ordenados por e-mail:**
    ```sql
    SELECT * FROM usuarios ORDER BY email ASC LIMIT 10;
    -- Retorna os 10 primeiros usuários ordenados alfabeticamente pelo e-mail
    ```

15. **Selecionar usuários cujo nome não contém a letra 'a':**
    ```sql
    SELECT * FROM usuarios WHERE nome NOT LIKE '%a%';
    -- Retorna os usuários cujo nome não possui a letra "a"
    ```

16. **Listar os nomes e e-mails, mas ordenando por nome decrescente:**
    ```sql
    SELECT nome, email FROM usuarios ORDER BY nome DESC;
    -- Retorna os nomes e e-mails dos usuários ordenados por nome em ordem decrescente
    ```

