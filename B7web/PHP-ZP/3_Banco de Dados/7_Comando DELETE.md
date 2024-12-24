
O comando `DELETE` é utilizado para remover registros de uma tabela em um banco de dados. Ele é uma ferramenta poderosa, mas deve ser usada com cautela para evitar a remoção acidental de dados importantes.

---

## **Estrutura Básica**
```sql
DELETE FROM tabela
WHERE condicao;
```
- `tabela`: A tabela de onde os registros serão excluídos.
- `condicao`: (Opcional) Uma condição que determina quais registros serão deletados.
  - **Se omitida**, todos os registros da tabela serão deletados!

---

## **1. Excluir registros com uma condição específica**
```sql
DELETE FROM tabela
WHERE coluna = 'valor';
-- Exclui os registros que atendem à condição especificada
```
### Exemplo:
```sql
DELETE FROM usuarios
WHERE id = 5;
-- Remove o usuário com ID igual a 5
```

---

## **2. Excluir todos os registros de uma tabela**
```sql
DELETE FROM tabela;
-- Remove todos os registros da tabela
```
### Exemplo:
```sql
DELETE FROM usuarios;
-- Remove todos os registros da tabela "usuarios"
```

**Nota:** Para limpar uma tabela completamente, o comando `TRUNCATE` é mais eficiente e seguro, pois não pode ser revertido.

---

## **3. Excluir registros com múltiplas condições**
```sql
DELETE FROM tabela
WHERE coluna1 = 'valor1' AND coluna2 = 'valor2';
-- Exclui os registros que atendem a todas as condições especificadas
```
### Exemplo:
```sql
DELETE FROM usuarios
WHERE nome = 'João' AND email = 'joao@email.com';
-- Remove o usuário chamado "João" com o e-mail "joao@email.com"
```

---

## **4. Excluir registros com uma condição mais ampla**
### **4.1 Excluir registros com base em um intervalo**
```sql
DELETE FROM tabela
WHERE coluna BETWEEN valor1 AND valor2;
-- Exclui os registros dentro do intervalo especificado
```
### Exemplo:
```sql
DELETE FROM usuarios
WHERE id BETWEEN 10 AND 20;
-- Remove os usuários cujos IDs estão entre 10 e 20
```

### **4.2 Excluir registros que correspondem a um padrão**
```sql
DELETE FROM tabela
WHERE coluna LIKE 'padrão';
-- Exclui os registros que correspondem ao padrão especificado
```
### Exemplo:
```sql
DELETE FROM usuarios
WHERE email LIKE '%@gmail.com';
-- Remove todos os usuários com e-mails do domínio "@gmail.com"
```

---

## **5. Excluir registros com base em valores únicos**
```sql
DELETE FROM tabela
WHERE coluna IN (valor1, valor2, ...);
-- Exclui os registros onde a coluna tem um dos valores especificados
```
### Exemplo:
```sql
DELETE FROM usuarios
WHERE id IN (1, 3, 5);
-- Remove os usuários com IDs 1, 3 e 5
```

---

# **Desafios Práticos**

## **Básicos**
1. **Excluir um registro com base no ID:**
   ```sql
   DELETE FROM usuarios
   WHERE id = 7;
   ```
   
2. **Remover todos os registros de uma tabela:**
   ```sql
   DELETE FROM usuarios;
   ```

3. **Excluir todos os usuários com o nome "Ana":**
   ```sql
   DELETE FROM usuarios
   WHERE nome = 'Ana';
   ```

## **Intermediários**
4. **Excluir usuários com e-mails terminando em `@yahoo.com`:**
   ```sql
   DELETE FROM usuarios
   WHERE email LIKE '%@yahoo.com';
   ```

5. **Remover registros com IDs menores que 5:**
   ```sql
   DELETE FROM usuarios
   WHERE id < 5;
   ```

6. **Excluir usuários cujos nomes começam com "J":**
   ```sql
   DELETE FROM usuarios
   WHERE nome LIKE 'J%';
   ```

7. **Remover todos os registros onde a coluna `ativo` está definida como `false`:**
   ```sql
   DELETE FROM usuarios
   WHERE ativo = false;
   ```

## **Avançados**
8. **Excluir registros com IDs entre 10 e 50:**
   ```sql
   DELETE FROM usuarios
   WHERE id BETWEEN 10 AND 50;
   ```

9. **Excluir usuários com nomes duplicados, mantendo apenas um registro de cada nome:**
   ```sql
   DELETE FROM usuarios
   WHERE id NOT IN (
       SELECT MIN(id) FROM usuarios
       GROUP BY nome
   );
   ```

10. **Excluir registros onde o nome não contém a letra "a":**
    ```sql
    DELETE FROM usuarios
    WHERE nome NOT LIKE '%a%';
    ```

---

# **Soluções dos Desafios**

### **1. Excluir um registro com base no ID**
```sql
DELETE FROM usuarios
WHERE id = 7;
```
**Explicação:** Remove apenas o registro com ID 7. 

### **2. Remover todos os registros de uma tabela**
```sql
DELETE FROM usuarios;
```
**Explicação:** Exclui todos os registros da tabela "usuarios". Use com cuidado!

### **3. Excluir todos os usuários com o nome "Ana"**
```sql
DELETE FROM usuarios
WHERE nome = 'Ana';
```
**Explicação:** Remove todos os registros onde o nome é "Ana".

---

# **Melhores Práticas**
1. **Sempre use a cláusula `WHERE`:** Para evitar excluir todos os registros acidentalmente.
2. **Teste o comando com `SELECT` antes:** Substitua `DELETE` por `SELECT` para verificar quais registros serão afetados.
3. **Faça backups regulares:** Sempre tenha backups atualizados antes de executar comandos que podem alterar permanentemente os dados.
4. **Evite deletar em cascata:** Use `ON DELETE CASCADE` com moderação em relacionamentos para evitar exclusões não intencionais.
5. **Use transações:** Se disponível, envolva o comando `DELETE` em uma transação para poder reverter se necessário:
   ```sql
   BEGIN TRANSACTION;
   DELETE FROM usuarios WHERE id = 10;
   ROLLBACK;
   
