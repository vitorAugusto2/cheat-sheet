# SQL 
---

## Índice

1. **DDL (Linguagem de Definição de Dados)**
   - [1.1 CREATE](#11-create)
   - [1.2 ALTER](#12-alter)
   - [1.3 DROP](#13-drop)
   - [1.4 TRUNCATE](#14-truncate)
   - [1.5 RENAME](#15-rename)

2. **DML (Linguagem de Manipulação de Dados)**
   - [2.1 INSERT](#21-insert)
   - [2.2 DELETE](#22-delete)
   - [2.3 UPDATE](#23-update)

## 1. DDL (Linguagem de Definição de Dados)

### 1.1 CREATE
Cria um novo objeto no banco de dados, como uma database, tabela e usuário 

```sql
-- Criar banco de dados
CREATE DATABASE nome_do_banco;

-- Criar schema
CREATE SCHEMA nome_do_schema;

-- Criar tabela
CREATE TABLE nome_da_tabela (
    coluna1 tipo_do_dado [restrições],
    coluna2 tipo_do_dado [restrições],
    ...
);

-- Criar usuário com senha
CREATE USER nome_do_usuario WITH PASSWORD 'senha';

-- Chave primária
PRIMARY KEY (nome_da_chave_primaria)

-- Chave estrangeira
FOREIGN KEY (nome_da_chave_primaria) REFRENCES schema.table(nome_da_coluna)
```

### 1.2 ALTER
Modifica a estrutura de um objeto existente, adiciona ou remove colunas de uma tabela

```sql
-- Adicionar uma coluna
ALTER TABLE nome_da_tabela
ADD coluna tipo_de_dado [restrições];

-- Remover uma coluna
ALTER TABLE nome_da_tabela
DROP COLUMN coluna;
```

### 1.3 DROP
Remove tabelas, databases e indices

```sql
-- Remove o índice 
ALTER TABLE nome_da_tabela 
DROP INDEX nome_do_indice;

-- Exclui a tabela 
DROP TABLE nome_da_tabela;

-- Exclui o banco 
DROP DATABASE nome_do_banco;
``` 

### 1.4 TRUNCATE
Remove todos os registros de uma tabela, mantendo sua estrutura

```sql
TRUNCATE TABLE nome_da_tabela;
```

### 1.5 RENAME
Comando utilizado para renomear tabelas

```sql
ALTER TABLE nome_da_tabela RENAME TO novo_nome
```

## 2. DML (Linguagem de Manipulação de Dados)

### 2.1 INSERT
Insere registros na tabela

```sql
INSERT INTO nome_da_tabela (atributo1, atributo2,..., atributo n)
VALUES (V1, V2, ..., VN)
```

### 2.2 DELETE
Remove registros na tabela

```sql
DELETE FROM tabela
WHERE predicado;
```

### 2.3 UPDATE
Atualiza registros na tabela

```sql
UPDATE <tabela>
SET atributo = xxxx
WHERE predicado;
```