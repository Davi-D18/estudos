# Anotações sobre o comando `INSERT`

O comando `INSERT` é usado para adicionar novos registros (linhas) em uma tabela de um banco de dados.

---

## **Estrutura Básica**
```sql
INSERT INTO tabela (coluna1, coluna2, ...) 
VALUES (valor1, valor2, ...);
```
- `tabela`: Nome da tabela onde os dados serão inseridos.
- `coluna1, coluna2`: As colunas nas quais os valores serão inseridos.
- `valor1, valor2`: Os valores correspondentes a serem adicionados.

Se todos os valores forem especificados na ordem das colunas da tabela, não é necessário declarar os nomes das colunas:
```sql
INSERT INTO tabela 
VALUES (valor1, valor2, ...);
```

---

## **1. Inserir um registro simples**
```sql
INSERT INTO usuarios (nome, email, senha) 
VALUES ('João Silva', 'joao@email.com', 'senha123');
-- Adiciona um registro com nome, email e senha
```
### Resultado:
- Insere uma nova linha na tabela `usuarios` com os valores especificados.

---

## **2. Inserir vários registros de uma vez**
```sql
INSERT INTO usuarios (nome, email, senha) 
VALUES 
  ('Ana Costa', 'ana@email.com', '12345'),
  ('Carlos Souza', 'carlos@email.com', 'qwerty'),
  ('Beatriz Lima', 'beatriz@email.com', 'abc123');
-- Adiciona múltiplos registros na tabela
```
### Resultado:
- Adiciona três registros simultaneamente na tabela `usuarios`.

---

## **3. Inserir sem especificar as colunas**
```sql
INSERT INTO usuarios 
VALUES ('Marcos Paulo', 'marcos@email.com', 'senha789');
-- Adiciona os valores em todas as colunas, respeitando a ordem da tabela
```
### Observação:
- Essa abordagem exige que você insira os valores na mesma ordem em que as colunas foram definidas na criação da tabela.

---

## **4. Inserir dados de outra tabela usando `SELECT`**
```sql
INSERT INTO novos_usuarios (nome, email) 
SELECT nome, email FROM usuarios WHERE email LIKE '%@gmail.com';
-- Copia dados da tabela "usuarios" para "novos_usuarios"
```
### Resultado:
- Insere registros em `novos_usuarios` com base nos dados filtrados da tabela `usuarios`.

---

## **5. Inserir valores nulos**
```sql
INSERT INTO usuarios (nome, email, senha) 
VALUES ('Pedro Silva', NULL, 'senha321');
-- Insere um registro com um valor nulo na coluna "email"
```
### Observação:
- `NULL` representa a ausência de valor e é usado para indicar que o dado não foi fornecido.

---

# **Desafios Práticos**

## **Básicos**
1. **Adicionar um novo usuário à tabela `usuarios`:**
   ```sql
   INSERT INTO usuarios (nome, email, senha) 
   VALUES ('Lucas Almeida', 'lucas@email.com', 'senha123');
   -- Adiciona o usuário Lucas Almeida
   ```

2. **Adicionar dois novos usuários com um único comando:**
   ```sql
   INSERT INTO usuarios (nome, email, senha) 
   VALUES 
     ('Maria Fernanda', 'maria@email.com', 'senha456'),
     ('Joana Pereira', 'joana@email.com', 'abc456');
   -- Adiciona Maria Fernanda e Joana Pereira
   ```

3. **Adicionar um usuário com um valor nulo no email:**
   ```sql
   INSERT INTO usuarios (nome, email, senha) 
   VALUES ('Carlos Dias', NULL, 'senha789');
   -- Adiciona Carlos Dias sem email
   ```

## **Intermediários**
4. **Copiar dados de `usuarios` para uma nova tabela chamada `backup_usuarios`:**
   ```sql
   INSERT INTO backup_usuarios (nome, email, senha) 
   SELECT nome, email, senha FROM usuarios;
   -- Copia todos os dados de "usuarios" para "backup_usuarios"
   ```

5. **Adicionar registros com diferentes padrões de email:**
   ```sql
   INSERT INTO usuarios (nome, email, senha) 
   VALUES 
     ('Amanda Silva', 'amanda@gmail.com', '123'),
     ('Ricardo Torres', 'ricardo@hotmail.com', '456');
   -- Adiciona registros com diferentes domínios de email
   ```

6. **Adicionar um registro e deixar a senha como `NULL`:**
   ```sql
   INSERT INTO usuarios (nome, email, senha) 
   VALUES ('Juliana Moreira', 'juliana@email.com', NULL);
   -- Insere Juliana Moreira sem uma senha definida
   ```

## **Avançados**
7. **Inserir dados de outro banco de dados:**
   ```sql
   INSERT INTO usuarios (nome, email, senha) 
   SELECT nome, email, senha FROM outro_banco.usuarios_externos;
   -- Copia dados de "usuarios_externos" para "usuarios"
   ```

8. **Inserir apenas parte dos dados de outra tabela:**
   ```sql
   INSERT INTO novos_usuarios (nome, email) 
   SELECT nome, email FROM usuarios WHERE senha LIKE '%123';
   -- Adiciona à tabela "novos_usuarios" apenas os dados filtrados
   ```

---

# **Dicas Importantes**

- **Boa prática:** Sempre especifique os nomes das colunas ao usar o `INSERT`. Isso evita erros caso a estrutura da tabela seja alterada.
- **Atenção:** Garanta que os tipos de dados nos valores correspondam aos tipos definidos para as colunas.
- **Chaves primárias:** Certifique-se de que os valores inseridos não violem as restrições de unicidade ou integridade da tabela.
- **Segurança:** Evite valores inseridos diretamente do usuário em aplicações (use parâmetros preparados para prevenir SQL Injection).
