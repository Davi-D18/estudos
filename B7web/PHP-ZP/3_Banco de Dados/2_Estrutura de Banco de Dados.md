
# **Anotações sobre Estrutura de um Banco de Dados**

## **1. Componentes de um Banco de Dados**

1. **Tabelas**:  
   - Onde os dados ficam guardados.  
   - Cada tabela tem **linhas** (informações) e **colunas** (categorias).  
   - **Exemplo de tabela de alunos**:
     ```
     | ID | Nome    | Idade | Cidade   |
     |----|---------|-------|----------|
     | 1  | João    | 25    | Recife   |
     | 2  | Maria   | 30    | Salvador |
     ```

2. **Colunas (Campos)**:  
   - Cada coluna representa um tipo de dado.  
   - Exemplo: "Nome" é texto (`VARCHAR`), "Idade" é número (`INT`).

3. **Linhas (Registros)**:  
   - Cada linha guarda as informações completas de um item ou pessoa.

4. **Chave Primária (Primary Key)**:  
   - Um identificador único para cada linha.  
   - Exemplo: "ID" na tabela de alunos.

5. **Chave Estrangeira (Foreign Key)**:  
   - Conecta tabelas diferentes.  
   - Exemplo: Uma tabela de pedidos pode se ligar à tabela de clientes.

6. **Índices**:  
   - Ajudam a encontrar dados rapidamente.  
   - Exemplo: Criar um índice para buscar alunos pelo nome.

---

## **2. Relacionamentos entre Tabelas**

Os relacionamentos conectam tabelas. Exemplos:

1. **Um para Um (1:1)**:  
   - Cada registro em uma tabela corresponde a apenas um em outra.  
   - Exemplo: Pessoa e seu Passaporte.

2. **Um para Muitos (1:N)**:  
   - Um registro em uma tabela pode ter vários registros na outra.  
   - Exemplo: Um cliente pode ter vários pedidos.

3. **Muitos para Muitos (N:M)**:  
   - Usamos uma tabela no meio para conectar as duas.  
   - Exemplo: Estudantes e Disciplinas. Tabela intermediária: "Matrículas".

---

## **3. Tipos de Dados**

Cada coluna tem um tipo de dado. Exemplos:

1. **Numéricos**:  
   - `INT`: Números inteiros. Exemplo: Idade = 25.  
   - `DECIMAL`: Números com casas decimais. Exemplo: Preço = 19.99.

2. **Texto**:  
   - `VARCHAR`: Texto curto. Exemplo: Nome = "João".  
   - `TEXT`: Texto longo. Exemplo: Descrição de produto.

3. **Data e Hora**:  
   - `DATE`: Apenas data. Exemplo: 2024-12-01.  
   - `DATETIME`: Data e hora. Exemplo: 2024-12-01 10:00:00.

4. **Booleano**:  
   - Valores verdadeiros ou falsos. Exemplo: Ativo = `TRUE`.

---

## **4. Normalização**

**Normalização** é organizar os dados para evitar repetições e erros.  

1. **Primeira Forma Normal (1NF)**:  
   - Cada dado deve estar em uma célula.  
   - **Errado**:  
     ```
     | Nome       | Telefones     |  
     |------------|---------------|  
     | João       | 123, 456      |  
     ```  
   - **Certo**:  
     ```
     | Nome       | Telefone      |  
     |------------|---------------|  
     | João       | 123           |  
     | João       | 456           |  
     ```  

2. **Segunda Forma Normal (2NF)**:  
   - Eliminar dados que não dependem da chave primária.  
   - Exemplo: Uma tabela de vendas deve separar informações do cliente.

3. **Terceira Forma Normal (3NF)**:  
   - Dados não devem depender de outras colunas além da chave primária.  
   - Exemplo: Uma tabela de alunos não deve ter informações de cursos repetidas.

---

## **5. Consultas com SQL**

**SQL** é a linguagem para interagir com o banco de dados. Exemplos básicos:

1. **Criar Tabela**:  
   ```sql
   CREATE TABLE Alunos (
       ID INT PRIMARY KEY,
       Nome VARCHAR(50),
       Idade INT
   );
   ```

2. **Inserir Dados**:  
   ```sql
   INSERT INTO Alunos (ID, Nome, Idade) VALUES (1, 'João', 25);
   ```

3. **Consultar Dados**:  
   ```sql
   SELECT * FROM Alunos;
   ```

4. **Atualizar Dados**:  
   ```sql
   UPDATE Alunos SET Nome = 'Maria' WHERE ID = 1;
   ```

5. **Excluir Dados**:  
   ```sql
   DELETE FROM Alunos WHERE ID = 1;
   ```

---

## **6. Restrições (Constraints)**

As restrições ajudam a garantir a qualidade dos dados. Exemplos:

1. **NOT NULL**:  
   - A coluna não pode ser vazia.  
   - Exemplo: O nome do aluno não pode ser nulo.

2. **UNIQUE**:  
   - Não permite valores repetidos.  
   - Exemplo: CPF.

3. **DEFAULT**:  
   - Define um valor padrão.  
   - Exemplo: Status padrão = "Ativo".

4. **CHECK**:  
   - Define regras.  
   - Exemplo: Idade deve ser maior que 0.

---

## **7. Backup e Recuperação**

1. **Backup**:  
   - Faz uma cópia dos dados para evitar perdas.  
   - Exemplo: Guardar o banco em um arquivo `.sql`.

2. **Recuperação**:  
   - Restaura o banco em caso de problemas.  

---

## **Resumo**

- **Tabelas** guardam os dados.  
- **Relacionamentos** conectam tabelas (1:1, 1:N, N:M).  
- **SQL** é usado para criar, modificar e consultar dados.  
- **Normalização** organiza os dados para evitar erros.  
- Restrições como **NOT NULL** e **UNIQUE** garantem a qualidade.
