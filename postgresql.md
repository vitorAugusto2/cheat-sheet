# PostgreSQL
**Termos**

- Palavra-chave: texto com significado em SQL (escrita em maiuscula) 
	+ Ex: `SELECT`, `FROM`, `JOIN`, `WHERE`, `ORDER BY`, ...
- Funções: tipo especial de palavra-chave.
	+ Ex: `COUNT()`, `YEAR()`, `SUM()`, `AVG()`, ...

- Identificadores: nome do objeto do banco de dados sendo uma tabela ou coluna (escrita em minúsculo e podendo usar _)
	+ Ex: 
		```sql
		SELECT a.**name** (coluna)
		FROM **animal** a (tabela)
		```
- Aliases: renomia uma tabela ou coluna temporiariamente
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
	+ Ex: 
		```sql
		  SELECT a.name      -- cláusula SELECT
		  FROM animal a      -- cláusula FROM
		  WHERE a.age > 5;   -- cláusula WHERE
		```
- Expressão: uma fórmula que resulta em um valor
	+ Ex:
		```sql
		COUNT(a.name)
		a.ano + 1
		```
- Predicados/Instruções Condicionais: comparação lógica que resulta em três valores -> TRUE/FALSE/UNKNOWN
	+ Ex:
		```sql
		a.nome = 'Rex'
		a.ano BETWEEN 1 AND 10
		a.nome IS NULL
		```

- Comentários: texto que é ignorado quando o código é executado
	+ Ex: 
		```sql
		-- Isso é um comentário
		SELECT * FROM animal;
		```
- Aspas:
	+ Simples -> 'Strings'
		```sql
		SELECT *
		FROM animal
		WHERE nome = 'Rex';
		```
	+ Duplas -> "Identificadores"
		```sql
		SELECT "name"
		FROM "animal";
		```
      
**Sublinguagens**

- DQL (Data Query Language): SELECT
- DDL (Data Definition Language): CREATE, ALTER e DROP
- DML (Data Manipulation Language): INSERT, UPDATE e DELETE
- DCL (Data Control Language): GRANTE e REVOKE
- TCL (Transactin Control Language): COMMIT e ROLLBACK

**Ordem de escrita**

1. SELECT
2. FROM
3. WHERE
4. GROUP BY
5. HAVING 
6. ORDER BY

**Ordem de execução**

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
-- 7.1) Correlacionadas:  referencia valores da consulta externa
SELECT
	column1,
	column2,
	(SELECT expression FROM table1) AS expression_name
FROM table1;

-- 7.2) Não Correlacionadas: nao referencia a consulta externa
SELECT
	column1,
	column2,
	(SELECT expression FROM table2 AS tb2
		WHERE tb1.column1 = tb2.column1) AS expression_name
FROM table1 AS tb1;

-- 8) DISTINCT
SELECT DISTINCT column1 
FROM table1;

-- 8.1) Contar números de valores exclusivos
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
-- buscar padrões em textos
-- % - qualquer número de caracteres
-- _ - um único caractere

-- 2.1) LIKE
SELECT
	column1
FROM table1
WHERE column1 LIKE 'Postgre%';

-- 2.2) NOT LIKE
SELECT
	column1
FROM table1
WHERE column1 NOT LIKE '%Postgre%';

-- 2.3) ILIKE
-- ignora maiúsculas e minúsculas
SELECT
	column1
FROM table1
WHERE column1 ILIKE '%Postgresql%';

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

### Avançado
---
#### **CASE, AGG, WINDOW FUNCTION e PIVOT**
```sql
-- 1) CASE
-- Lógica if-else
SELECT
	CASE
		WHEN condition THEN result
		WHEN condition THEN result
		...
		ELSE standard_result
	END AS name_column;

-- 1.1) COALESCE + CASE
-- Substitui todos os valores NULL de uma coluna por um valor diferente
SELECT
	COALESCE(
		CASE
			WHEN condition THEN result
			WHEN condition THEN result
			...
			ELSE standard_result
		END,
		'null'
	) AS name_column;

-- 2) GROUP BY

```
## **DDL**
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
## **DML** 

## **TCL**
### **Transaction**
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


## **Tipos de Dados**
### **Dados numéricos**
 
| Inteiros       | Decimal            | Flutuante        |
|----------------|--------------------|------------------|
| SMALLINT       | DECIMAL ou NUMERIC | REAL             |
| INT ou INTEGER |					  | DOUBLE PRECISION |	
| BIGINT         |					  |                  |
| SMALLSERIAL    |                    |					 |
| SERIAL         |                    |					 |
| BIGSERIAL      |                    |					 |

### **Dados de string**
```sql
'This is a string'
'You're welcome.'

$$This is a string.$$
$mytag$This is a string.$mytag$
```

| Sequência de escape | Descrição        |
|---------------------|------------------|
| \'        		  | Aspa simples     |
| \t       			  | Tabulação        |
| \n        		  | Nova linha       |
| \r        		  | Retorno de carro |
| \b        	  	  | Backspace        |
| \\        		  | Barra invertida  |

| Tipo de dado | 
|--------------|
| CHAR         | 
| VARCHAR      |


### **Datatime**
| Data 				  	    		   | Tempo                         | Data e Hora 							       |
|--------------------------------------|-------------------------------|-----------------------------------------------|
| SELECT DATE '2021-02-25';            | SELECT TIME '10:30';          | SELECT TIMESTAMP '2021-02-25 10:30';	       |
| SELECT DATE('2021-0225');            | SELECT CAST('10:30' AS TIME); | SELECT CAST('2021-02-25 10:30' AS TIMESTAMP); |
| SELECT CAST('2021-02-2025' AS DATE); |							   |											   |

| Tipo de dado             | Descrição                      |
|--------------------------|--------------------------------|
| DATE                     | YYYY-MM-DD                     |
| TIME                     | HH:MM:SS                       |
| TIME WITH TIME ZONE      | HH:MM:SS (-+) H:MM             |
| TIMESTAMP                | YYYY-MM-DD HH:MM:SS            |
| TIMESTAMP WITH TIME ZONE | YYYY-MM-DD HH:MM:SS (-+) H:MM  |

### **Outros**
| Boolean | Binário |
|---------|---------|
| BOOLEAN | BYTEA   |


## **Operadores e Funções**
| Operadores lógicos   | Operadores de comparacação (símbolos)       | Operadores de comparação (palavras-chaves)         | Operadores matemáticos        |
|----------------------|---------------------------------------------|----------------------------------------------------|-------------------------------|
| AND <br> OR <br> NOT | = <br> !=, <> <br> < <br> <= <br> > <br> >= | BETWEEN <br> EXISTS <br> IN <br> IS NULL <br> LIKE | + <br> - <br> * <br> / <br> % |

| Funções de agregação                                | Funções numéricas                                                                                                                                           | Funções de string                                                                                                    | Funções de data e hora                                | Funçõe de valores nulos |
|-----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|-------------------------|
| COUNT() <br> SUM() <br> AVG() <br> MIN() <br> MAX() | ABS() <br> SIGN() <br> POWER <br> SQRT() <br> EXP() <br> LOG() <br> LN() <br> MOD() <br> PI() <br> COS() <br> SIN() <br> RANDOM() <br> ROUND() <br> CAST()  | LENGTH() <br> UPPER(), LOWER() <br> TRIM(), LTRIM(), RTRIM() <br> CONCAT() <br> SUBSTR() <br> REPLACE() <br> REGEXP  | CURRENT_DATE <br> CURRENT_TIME <br> CURRENT_TIMESTAMP | COALCASE()              |

### **Expressões Regulares**
```sql
--SIMILAR TO ou ~: procurar padrão de expressão regular

-- 1) Com SIMILAR
SELECT *
FROM table1
WHERE column1 SIMILAR TO '(<expressao>)';

-- 2) Com ~
SELECT *
FROM table1
WHERE column1 ~'<expressao>';

```




 
