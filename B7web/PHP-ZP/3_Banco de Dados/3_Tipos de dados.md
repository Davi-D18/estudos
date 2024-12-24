
# **Anotações sobre Tipos de Dados no phpMyAdmin**

O phpMyAdmin é uma ferramenta para gerenciar bancos de dados MySQL. Entender os tipos de dados é essencial para criar tabelas bem estruturadas.

---

## **1. Categorias de Tipos de Dados**

1. **Numéricos**: Para números (inteiros ou decimais).  
2. **Texto**: Para palavras, frases e grandes blocos de texto.  
3. **Data e Hora**: Para armazenar datas, horas ou ambos.

---

## **2. Tipos Numéricos**

1. **Para números inteiros**:  
   - **TINYINT**: Números pequenos (0 a 255 com `UNSIGNED`).  
     _Exemplo_: Idade de uma pessoa.  
   - **INT**: Padrão para números inteiros grandes (-2 bilhões a 2 bilhões).  
     _Exemplo_: IDs únicos.  
   - **BIGINT**: Para números gigantes.  
     _Exemplo_: Saldo bancário.  

2. **Para números com casas decimais**:  
   - **FLOAT**: Menos preciso. _Exemplo_: Temperaturas.  
   - **DECIMAL**: Alta precisão. _Exemplo_: Preços (10.99).

---

## **3. Tipos de Texto**

1. **Tamanho pequeno**:  
   - **VARCHAR(tamanho)**: Texto de tamanho variável (até 65.535 caracteres).  
     _Exemplo_: Nome de usuários.  
   - **CHAR(tamanho)**: Texto de tamanho fixo (até 255 caracteres).  
     _Exemplo_: Códigos como "ABC123".  

2. **Blocos de texto maiores**:  
   - **TEXT**: Para descrições maiores (até 65.535 caracteres).  
     _Exemplo_: Descrições de produtos.  
   - **LONGTEXT**: Para textos gigantes (até 4 GB).  
     _Exemplo_: Artigos de blogs.  

3. **Listas fixas**:  
   - **ENUM**: Lista de valores únicos.  
     _Exemplo_: Status ('Ativo', 'Inativo').  
   - **SET**: Lista de múltiplos valores pré-definidos.  
     _Exemplo_: Dias de entrega ('Segunda', 'Quarta').

---

## **4. Tipos de Data e Hora**

1. **DATA**: Apenas a data (`YYYY-MM-DD`).  
   _Exemplo_: `1995-08-15`.  

2. **DATETIME**: Data e hora (`YYYY-MM-DD HH:MM:SS`).  
   _Exemplo_: `2024-12-01 10:30:00`.  

3. **TIME**: Apenas a hora (`HH:MM:SS`).  
   _Exemplo_: `08:30:00`.  

4. **YEAR**: Apenas o ano (`YYYY`).  
   _Exemplo_: `2024`.  

---

## **5. Dicas para Escolher os Tipos de Dados**

1. **Escolha o menor tipo possível**:  
   - Use `TINYINT` para valores pequenos e `VARCHAR` para textos curtos.  

2. **Defina valores obrigatórios com `NOT NULL`**:  
   - Use quando o dado não pode ficar vazio.  

3. **Use `UNSIGNED` para valores positivos**:  
   - Exemplo: Idade ou quantidade (sem negativos).  

4. **Automatize IDs com `AUTO_INCREMENT`**:  
   - Crie identificadores únicos automaticamente.  

5. **Evite exagerar no tamanho**:  
   - Não use `TEXT` ou `LONGTEXT` se `VARCHAR` for suficiente.

---

## **6. Exemplo de Tabela no phpMyAdmin**

### **Definição da tabela "Alunos"**:
- Campos:  
  - `id`: `INT`, chave primária, `AUTO_INCREMENT`.  
  - `nome`: `VARCHAR(50)`, obrigatório (`NOT NULL`).  
  - `idade`: `TINYINT`, apenas valores positivos (`UNSIGNED`).  
  - `data_cadastro`: `DATETIME`, padrão `CURRENT_TIMESTAMP`.  

### **SQL Gerado**:
```sql
CREATE TABLE Alunos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL,
    idade TINYINT UNSIGNED,
    data_cadastro DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

---

## **Resumo**

- Tipos de dados são importantes para organizar bem o banco.  
- Planeje antes de criar a tabela. Escolha o tipo certo para cada dado.  
- Pratique no phpMyAdmin e veja os SQL gerados para entender como funciona.
