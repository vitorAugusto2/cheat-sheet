# POSTGRESQL
* Termos
	- Palavra-chave: texto com significado em SQL
		+ Ex: SELECT, FROM, INNER JOIN, ...
	- Funções: tipo especial de palavra-chave.
		+ Ex: COUNT(), YEAR(), ...

	- Identificadores: nome do objeto do banco de dados sendo uma tabela ou coluna
		+ Ex: 
			```sql
			SELECT a.**name** (coluna)
			FROM **animal** a (tabela)
			```
	- Aliases: renomia uma tabela ou coluna temporiariamente; **Emoji joinha**
		+ Ex:
			```sql
			SELECT a.name 
			FROM animal **AS** a (alias)
			```
    - Instruções: começa com palavra-chave e termina com ponto e vírgula
    	+ Ex:
    		```sql
			**SELECT a.name 
			FROM animal AS a;**
			```
	- Cláusula: um pedaço de uma instrução
		+ Ex: "Cláusula SELECT", "Cláusula WHERE", ...

	- Expressão: uma fórmula que resulta em um valor
		+ Ex:
		    ```sql
			COUNT(a.name)
			```
	- Predicados/Instruções Condicionais: comparação lógica que resulta em três valores -> TRUE/FALSE/UNKNOWN
		+ Ex: **colocar algum exemplo**

	- Comentários: texto que é ignorado quando o código é executado
		+ Ex: 
		```sql-- Isso é um comentário```
	- Aspas:
		+ Simples -> 'Strings'
		+ Duplas -> "Identificadores"

* Sublinguagens
	- DQL (Data Query Language): SELECT
	- DDL (Data Definition Language): CREATE, ALTER e DROP
	- DML (Data Manipulation Language): INSERT, UPDATE e DELETE
	- DCL (Data Control Language): GRANTE e REVOKE
	- TCL (Transactin Control Language): COMMIT e ROLLBACK

* Ordem de escrita
	1. SELECT
	2. FROM
	3. WHERE
	4. GROUP BY
	5. HAVING 
	6. ORDER BY

* Ordem de execução
	1. FROM
	2. WHERE
	3. GROUP BY
	4. HAVING
	5. SELECT 
	6. ORDER BY

## DQL
### **SELECT**
```sql
-- SELECT: colunas que queremos que uma instrução retorne
--
-- 1) Selecionando colunas
SELECT
	column1,
	column2
FROM table1;

-- 2) Selecionando todas as colunas
SELECT * 
FROM table1;

-- 3) Selecionando expressões
SELECT
	column1,
	expression --ROUND(population * 0.9, 0)
FROM table1;

-- 4) Selecionando funções
SELECT function; --CURRENT_DATE

-- 5) Atribuindo aliases
SELECT
	column1,
	column2
FROM table1 AS tb1;

-- 6) Notação de ponto: coluna e tabela
SELECT
	tb1.column1,
	tb1.column2
FROM dbo.table1 AS tb1;

-- 7) Subconsultas
-- 7.1) Correlacionadas
SELECT
	column1,
	column2,
	(SELECT expression FROM table1) AS expression_name
FROM table1;

-- 7.2) Não Correlacionadas
SELECT
	column1,
	column2,
	(SELECT expression FROM table2 AS tb2
		WHERE tb1.column1 = tb2.column1) AS expression_name
FROM table1 AS tb1;

-- 8) DISTINCT
SELECT DISTINCT column1 
FROM table1;

SELECT COUNT(*) AS num_total
FROM table1;

SELECT COUNT(DISTINCT(column1, column2)) AS unique
FROM table1;
```

### **FROM**
```sql
-- FROM: fonte de dados (tabela) que queremos recuperar
--
-- 1) Selecionando tabela
SELECT
	column1,
	column2
FROM table1;

-- 2) De várias tabelas
SELECT * 
FROM table1 AS tb1
	JOIN table2 AS tb2 ON tb2.id = tb1.id;

-- 3) Subconsulta/Tabela Derivada
SELECT 
	tb1.column1 AS name1
	tb2.column1 AS name2
	
FROM (SELECT * FROM table2 WHERE column1 = 'NULL') AS tb2
	JOIN table1 AS tb1 ON tb1.id = tb2.id;
```

### **WHERE**
```sql
-- WHERE: filtragem de dados
--
-- 1) Filtrar por uma coluna
SELECT *
FROM table1
WHERE column1 = 1
LIMIT 10;

-- 2) Utilizando LIKE
SELECT
	column1,
	column2
FROM table1
WHERE column1 NOT LIKE '%Postgre%';

-- 3) Vários predicados com operadores
SELECT
	column1,
	column2
FROM table1
WHERE
	column1 NOT LIKE '%Postgre%'
	AND column2 = "SQL";
```

### **GROUP BY**
```sql
-- GROUP BY: agrupar dados que são parecidos, geralmente fazer algum tipo de calculo
--
-- 1) Agrupar
SELECT
	tb1.column1,
	COUNT(*) AS num_total
FROM table1 AS tb1
GROUP BY tb1.column1;
```

### **HAVING**
```sql
-- HAVING: restrições para linhas qunado tiver GROUP BY
--
-- 1) Restrição
SELECT
	tb1.column1,
	COUNT(*) AS num_total
FROM table1 AS tb1
GROUP BY tb1.column1
HAVING COUNT(*) = 10;
```

### **ORDER BY**
```sql
-- ORDER BY: classificar/ordenar os dados
--
-- 1) Classificar
-- 1.1) Ascendente
SELECT
	tb1.column1,
	COUNT(*) AS num_total
FROM table1 AS tb1
GROUP BY tb1.column1
ORDER BY tb1.column1 ASC;

-- 1.2) Descendente
SELECT
	tb1.column1,
	COUNT(*) AS num_total
FROM table1 AS tb1
GROUP BY tb1.column1
ORDER BY tb1.column1 DESC;

-- 2) Posição numérica
SELECT
	tb1.column1,
	COUNT(*) AS num_total
FROM table1 AS tb1
GROUP BY tb1.column1
ORDER BY
	1 DESC,
	2 ASC;
```

### **LIMIT**
```sql
-- LIMIT: limitar o número de linhas vizualizado
--
-- 1) Limitar
SELECT *
FROM table1
WHERE column1 = 1
LIMIT 10;
```

## DDL
### **DB**
```sql
-- 1) Exibir nome de Banco de Dados existentes
\l 

-- 2) Exibir nome de Banco de Dados atual
SELECT current_database();

-- 3) Mudar de Banco de Dados
\c another_db 

-- 4) Criar Banco de Dados
CREATE DATABASE my_new_db;

-- 5) Excluir Banco de Dados
DROP DATABASE my_new_db;
```



### **CREATE**
```sql
-- 1) Criar tabela
-- Restrições: NOT NULL, DEFAULT, CHECK, UNIQUE, PRIMARY KEY, FOREIGN KEY
CREATE TABLE name_table (
	column1 TYPE restriction,
	column2 TYPE restriction,
...
); 

-- 2) Inserir linhas
INSERT INTO name_table (column1, column2, ...)
VALUES
	(value1, value2, ...)
	(value1, value2, ...)
	(value1, value2, ...);

-- 3) Exibir nomes das tabelas existentes
\dt

-- 4) Criar tabela que não existe
CREATE TABLE IF NOT EXISTS name_table (
	column1 TYPE restriction,
	column2 TYPE restriction,
...
); 

-- 5) Excluir:
-- 5.1) Totalmente
DROP TABLE name_table;

-- 5.2) Mantar a estrutura (truncar)
DELETE FROM name_table;

-- 5.3) Referencia a chave estrangeira
DELETE FROM name_table CASCADE;

-- 6) Chaves primária e estrangeira
-- 6.1) Chave primária: identifica de maneira exclusiva cada linha de dados
CREATE TABLE name_table1 (
	column1_id TYPE PRIMARY KEY
	...
); 

-- Ou composta
CREATE TABLE name_table1 (
	column1_id  TYPE restriction,
	column2_id  TYPE restriction,
	...
	CONSTRAINT pk_id1
	PRIMARY KEY(column1_id, column2_id)
); 
-- 6.2) Chave estrangeira: referencia uma chave primária de outra tabela
CREATE TABLE name_table1 (
	column1_id TYPE PRIMARY KEY
	...
); 

CREATE TABLE name_table2 (
	id 		TYPE restriction,
	column2_id TYPE restriction,
	...
	FOREIGN KEY(column2_id)
	REFERENCES(column1_id)
);

-- 7) Gerar automaticamente
CREATE TABLE name_table(
	id SERIAL,
	column2 TYPE restriction,
	...
);

-- 8) Inserção de dados de um arquivo de texto em uma tabela 
\copy new_table 
	FROM '<file_path>/my_data.csv'
	DELIMITER ',' CSV HEADER
```

### **UPDATE**
```sql
-- 1) Renomeação 
-- 1.1) Tabela
ALTER TABLE old_table_name
RENAME TO new_table_name;

-- 1.2) Coluna 
ALTER TABLE my_table
	RENAME COLUMN old_column_name
	TO new_column_name;

-- 2) Exibição
\d my_table

-- 3) Inclusão
ALTER TABLE my_table
	ADD new_num_columnn INTEGER,
	ADD new_text_column VARCHAR(30);

-- 4) Exclusão
ALTER TABLE my_table
	DROP COLUMN new_num_columnn,
	DROP COLUMN new_text_column;
```

### **INDEX**
```sql
-- 1) Criação para acelerar consultas
CREATE INDEX my_index ON my_table (column1, column2, ...);

-- 2) Exclusão
DROP INDEX my_index;                                                     
```

### **VIEW**
```sql
-- 1) Criação
CREATE VIEW name_view AS
	query;

-- 2) Atualizar
CREATE OR REPLACE name_view AS
	query;

-- 3) Exclusão
DROP VIEW name_view;

-- 4) Exibir todas as view existentes
SELECT table_name
FROM information_schema.views
WHERE table_schema NOT IN
	('information_schema', 'pg_catalog');
```

### **TRANSAÇÕES**
```sql
-- 1. Iniciar transação
START TRANSACTION;
-- or
BEGIN;

-- 2. Alterações
query;

-- 3. Testes
query;

-- 4.1. Confirmar Alterações
COMMIT;
-- or
-- 4.2. Desfazer Alterações
ROLLBACK;  
```
