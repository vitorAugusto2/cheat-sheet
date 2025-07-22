# SQL 
---

## Índice

![sql_language](https://github.com/user-attachments/assets/d5370e6a-5c60-44cd-a7fa-3ba7446f9814)

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
PRIMARY KEY (nome_da_chave_primaria);

-- Chave estrangeira
FOREIGN KEY (nome_da_chave_primaria) REFERENCES nome_da_tabela(nome_da_coluna);
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
DELETE FROM nome_da_tabela
WHERE predicado;
```

### 2.3 UPDATE
Atualiza registros na tabela

```sql
UPDATE nome_da_tabela
SET atributo = xxxx
WHERE predicado;
```

### 2.4 CASCADE
Excluir ou atualizar os registros relacionados presentes nas tabelas referenciadas.

Outros: `RESTRICT`, `SET NULL`, `NO ACTION` e `SET DEFAULT`

```sql
ALTER TABLE nome_da_tabela
ADD CONSTRAINT nome_da_coluna_fk 
FOREIGN KEY (nome_da_chave_primaria) REFERENCES nome_da_tabela(nome_da_coluna)
ON DELETE CASCADE;
```

## 3. DQL (Linguagem de Consulta de Dados)

### 3.1 SELECT
Consultar os dados no armazenados no banco

```sql
-- Lista os atributos desejados de uma consulta
SELECT atributo1, atributo2, ..., atributoN
FROM relacao1, relacao2, ..., relacaoN
WHERE predicado   

-- Valores unicos
SELECT DISTINCT(atributo1)
FROM relacao1


-- Selecionar todos os atributos
SELECT * 
FROM relacao1, relacao2, ..., relacaoN
WHERE predicado

-- Where: especifica a condição que a resposta da consulta deve conter
SELECT *
FROM atributo1, atributo2
WHERE atributo1 > atributo2 AND atributo1 = predicado
``` 


### 3.2 RENAME AS
Renomea as colunas 

```sql
SELECT atributo1, atributo2, ..., atributoN
FROM relacao1 AS a, relacao2 AS b, ..., relacaoN as z
WHERE relacao1.a = releacao2.b, ..., relacaoN.z predicado;
```

```sql
-- Usando alias
SELECT atributo1, atributo2, ..., atributoN
FROM relacao1 as a, relacao2 as, ..., relacaoN
WHERE r1.a = r2.a AND r3.a = rm.a AND ... predicado;
```

### 3.3 JOINS
```sql
-- INNER JOIN: entre valores comuns
SELECT * FROM a
INNER JOIN b  ON a.key = b.key

-- LEFT JOIN
SELECT * FROM a 
LEFT JOIN b ON a.key = b.key

SELECT * FROM a
LEFT JOIN b ON a.key = b.key
WHERE b.key IS NULL

-- RIGHT JOIN
SELECT * FROM a
RIGHT JOIN b ON a.key = b.key

SELECT * FROM a
RIGHT JOIN b ON a.key = b.key
WHERE a.key IS NULL

-- FULL JOIN
SELECT * FROM a
FULL JOIN b ON a.key = b.key

SELECT * FROM a
FULL JOIN b ON a.key = b.key
WHERE a.key IS NULL OR b.key IS NULL 
```

## 3.4 AGREGAÇÕES 

```sql
-- agg: MAX, MIN, AVG e COUNT
SELECT * AGG(atributo)
FROM relacao
WHERE predicado

-- Group By
SELECT * AGG(atributo1), atributo2
FROM relacao1, relacao2
GROUP BY predicado

-- Order By - ASC/DESC: ordenar menor ou maior
SELECT * AGG(atributo1), atributo2
FROM relacao1, relacao2
ORDER BY predicado ASC

-- LIMIT
SELECT * AGG(atributo1), atributo2
FROM relacao1, relacao2
ORDER BY predicado DESC LIMIT 2

-- HAVING
SELECT * AGG(atributo1), atributo2
FROM relacao1, relacao2
GROUP BY predicado
HAVING AGG(predicado)

-- UNION
SELECT * FROM releacao1
WHERE predicado1

UNION

SELECT * FROM relacao2
WHERE predicado2

-- INTERSECT
SELECT * FROM releacao1
WHERE predicado1

INTERSECT   

SELECT * FROM relacao2
WHERE predicado2

-- EXCEPT
SELECT * FROM releacao1
WHERE predicado1

EXCEPT

SELECT * FROM relacao2
WHERE predicado2
```