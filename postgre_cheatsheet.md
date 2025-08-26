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
