# PANDAS


## Índice

1. [Introdução ao Pandas](#introducao-ao-pandas)
   - [1.1 Séries](#11-series)
   - [1.2 DataFrame](#12-dataframe)
   - [1.3 Objetos Index](#13-objetos-index)
   - [1.4 Funcionalidade Essenciais](#14-funcionalidade-essenciais)
     - [1.4.1 Reindexação](#141-reindexacao)
     - [1.4.2 Remoção de entradas de um eixo](#142-remocao-de-entradas-de-um-eixo)
     - [1.4.3 Indexação com loc e iloc](#143-indexacao-com-loc-e-iloc)
     - [1.4.4 Ordenação e Classificação](#144-ordenacao-e-classificacao)
     - [1.4.5 Estatística Descritiva](#145-estatistica-descritiva)

2. [Carregamento de Dados, Armazenamento e Formatos de Arquivos](#carregamento-de-dados-armazenamento-e-formatos-de-arquivos)
   - [2.1 Leitura e Escrita de Dados no Formato Texto](#21-leitura-e-escrita-de-dados-no-formato-texto)
   - [2.2 Interações](#22-interacoes)
     - [2.2.1 Web APIs](#221-web-apis)
     - [2.2.2 Banco de Dados](#222-banco-de-dados)

3. [Limpeza e Preparação dos Dados](#limpeza-e-preparacao-dos-dados)
   - [3.1 Manipulação de Dados Ausentes](#31-manipulacao-de-dados-ausentes)
   - [3.2 Transformação de Dados](#32-transformacao-de-dados)
   - [3.3 Manipulação de Strings](#33-manipulacao-de-strings)

4. [Junção, Combinação e Reformatação](#juncao-combinacao-e-reformatacao)
   - [4.1 Indexação Hierárquica](#41-indexacao-hierarquica)
   - [4.2 Agrupamento de Dados](#42-agrupamento-de-dados)
   - [4.3 Combinação e Mesclagem de Conjuntos de Dados](#43-combinacao-e-mesclagem-de-conjuntos-de-dados)
     - [4.3.1 Concatenação ao Longo de um Eixo](#431-concatenacao-ao-longo-de-um-eixo)
   - [4.4 Reformatação e Pivotamento](#44-reformatacao-e-pivotamento)
     - [4.4.1 Reformatação](#441-reformatacao)
     - [4.4.2 Pivotamento](#442-pivotamento)


## 1. Introdução ao Pandas



O pandas é uma biblioteca poderosa para manipulação e análise de dados em Python. Ele oferece estruturas de dados flexíveis, como `Series` , `DataFrame` e `Index`, que permitem trabalhar com dados de forma eficiente.

```python
# Biblioteca Pandas
# Instalação
pip install pandas

# Importação
import pandas as pd
```

### **1.1 Séries**

Uma `Series` é uma sequência unidimensional de valores (semelhante a um array) com rótulos chamados de índice.

```python
# Criação de uma Série com pandas
#
# Sintaxe: pd.Series(data=None, index=None, dtype=None, name=None, copy=None)
#
# Parâmetros:
# - data: Dados que serão inseridos na Série (pode ser uma lista, array NumPy, dicionário, etc.)
# - index: Índices personalizados para a Série.
# - dtype: Tipo de dado específico para a Série.
# - name: Nome da Série.
# - copy: Cria uma cópia dos dados, útil para evitar modificar o objeto original.
# - fastpath: Parâmetro interno utilizado pelo pandas para otimizar a criação de Séries (não é necessário ajustar na maioria dos casos).

# Exemplo 1: Criando uma Série a partir de uma lista
data = [10, 20, 30, 40]
index = ["a", "b", "c", "d"]
series = pd.Series(data=data, index=index)

# Exemplo 2: Criando uma Série a partir de um dicionário
data_dict = {"a": 100, "b": 200, "c": 300}
series_from_dict = pd.Series(data=data_dict, dtype="float64", name="From Dictionary")

# Exemplo 3: Criando uma Série vazia com tipo específico
empty_series = pd.Series(dtype="float64", name="Empty Series")

# Exemplo 4: Criando uma Série e forçando uma cópia dos dados
data_copy = [5, 10, 15]
series_with_copy = pd.Series(data=data_copy, copy=True, name="Copied Series")

# Observação:
# - Quando o parâmetro `dtype` não é especificado, pandas tenta inferir o tipo de dado automaticamente.

```

### **1.2 DataFrame**

O `DataFrame` é uma tabela bidimensional com colunas nomeadas e indexadas. Ele pode ser visto como um dicionário de `Series` alinhadas. Cada coluna pode conter tipos de dados diferentes.

```python
# Criação de um DataFrame com pandas
#
# Sintaxe: pd.DataFrame(data=None, index=None, columns=None, dtype=None, copy=None)
#
# Parâmetros:
# - data: Os dados para o DataFrame (pode ser uma lista de listas, dicionário, array NumPy, outra estrutura de dados, etc.).
# - index: Personaliza os índices das linhas. Se não for especificado, pandas usa o padrão (inteiros começando de 0).
# - columns: Define os rótulos das colunas. Se não for especificado, pandas usa valores numéricos padrão como rótulos.
# - dtype: Especifica o tipo de dado para todas as colunas.
# - copy: Faz uma cópia dos dados, útil para evitar que o DataFrame modifique a estrutura original.

# Exemplo 1: Criando um DataFrame a partir de uma lista de listas
data = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
columns = ["A", "B", "C"]
df_from_list = pd.DataFrame(data=data, columns=columns)

# Exemplo 2: Criando um DataFrame a partir de um dicionário de listas
data_dict = {"A": [1, 4, 7], "B": [2, 5, 8], "C": [3, 6, 9]}
df_from_dict = pd.DataFrame(data=data_dict)

# Exemplo 3: Criando um DataFrame com índice e colunas personalizadas
index = ["Linha 1", "Linha 2", "Linha 3"]
df_custom_index = pd.DataFrame(data=data, columns=columns, index=index)

# Exemplo 4: Criando um DataFrame a partir de um array NumPy e especificando o tipo de dado
data_array = np.array([[1.5, 2.5, 3.5], [4.5, 5.5, 6.5]])
df_from_array = pd.DataFrame(data=data_array, columns=["X", "Y", "Z"], dtype="float32")

# Exemplo 5: Criando um DataFrame vazio com colunas pré-definidas
empty_df = pd.DataFrame(columns=["Coluna 1", "Coluna 2"])

# Exemplo 6: Criando um DataFrame e forçando a cópia dos dados
data_copy = {"Coluna 1": [10, 20], "Coluna 2": [30, 40]}
df_with_copy = pd.DataFrame(data=data_copy, copy=True)
```

### **1.3 Objetos Index**

Um `Index` contém os rótulos dos eixos e outros metadados. Eles são imutáveis e usados para alinhar dados.

```python
# Criação de um Index com pandas
#
# Sintaxe: pd.Index(data=None, dtype=None, copy=False, name=None, tupleize_cols=True)
#
# Parâmetros:
# - data: Os dados para o Index (pode ser uma lista, array NumPy, ou outra estrutura de dados).
# - dtype: Especifica o tipo de dado do Index (por exemplo, 'int64', 'float64', 'object' para strings, etc.).
# - copy: Se True, cria uma cópia dos dados ao invés de usar a referência original.
# - name: Um nome para o Index, útil quando se trabalha com múltiplos Indexes nomeados.
# - tupleize_cols: Se True, converte múltiplas colunas em tuplas (relevante em Indexes multi-níveis).

# Exemplo 1: Criando um Index simples a partir de uma lista
data = [10, 20, 30, 40]
index = pd.Index(data=data, name="Sample Index")

# Exemplo 2: Criando um Index a partir de um array NumPy e especificando o tipo de dado
data_array = np.array([1.5, 2.5, 3.5, 4.5])
index_from_array = pd.Index(data=data_array, dtype="float32", name="Float Index")

# Exemplo 3: Criando um Index com cópia dos dados forçada
index_copy = pd.Index(data=[5, 10, 15], copy=True, name="Copied Index")

# Exemplo 4: Criando um Index multi-nível usando tupleize_cols
multi_level_data = [(1, "A"), (2, "B"), (3, "C")]
multi_level_index = pd.Index(data=multi_level_data, tupleize_cols=True, name="Multi-Level Index")

# Exemplo 5: Criando um Index vazio com tipo específico
empty_index = pd.Index(dtype="int64", name="Empty Index")

# Observações:
# - `name` é útil para identificar um Index quando você trabalha com DataFrames que possuem múltiplos índices (como em multi-índices).
# - `tupleize_cols=True` é especialmente importante ao trabalhar com dados hierárquicos ou multi-índices.
# - `copy` é útil quando você não deseja modificar a estrutura original dos dados.
```

### **1.4 Funcionalidade essencias**

#### 1.4.1 Reindexação

Cria um novo objeto com os valores reorganizados para ficarem alinhados com o novo índice. Pode alterar o índice das linhas, colunas, ou ambos.

```python
# Método reindex para ajustar o índice ou colunas de um DataFrame ou Série
#
# Sintaxe: reindex(labels, index, columns, axis, method, fill_value, limit, tolerance, level, copy)
#
# Parâmetros:
# - labels: Os novos rótulos do índice ou colunas para reindexar.
# - index: Alternativa para o parâmetro "labels", usado quando você deseja especificar o novo índice.
# - columns: Os novos rótulos das colunas para reindexar.
# - axis: Especifica o eixo de aplicação (0 para linhas e 1 para colunas).
# - method: Método de preenchimento dos valores ausentes após a reindexação. Pode ser "ffill" (propagar valores anteriores) ou "bfill" (propagar valores seguintes).
# - fill_value: Valor com o qual preencher os dados ausentes resultantes da reindexação.
# - limit: Limita o número de valores preenchidos ao usar "ffill" ou "bfill".
# - tolerance: Tolerância para o preenchimento ao fazer o "reindex" (geralmente útil em Séries com índice numérico).
# - level: Reindexa ao nível de um MultiIndex.
# - copy: Se True, cria uma cópia dos dados, mesmo que o índice já esteja alinhado corretamente.

# Exemplo 1: Reindexando um DataFrame para adicionar novas linhas com valores ausentes
data = {"A": [1, 2, 3], "B": [4, 5, 6]}
index = ["a", "b", "c"]
df = pd.DataFrame(data, index=index)

new_index = ["a", "b", "c", "d", "e"]  # Adicionando novas linhas "d" e "e"
df_reindexed = df.reindex(labels=new_index, fill_value=0)  # Preenche os valores ausentes com 0

# Exemplo 2: Reindexando colunas e preenchendo valores ausentes com NaN
new_columns = ["A", "B", "C"]  # Adicionando a coluna "C"
df_reindexed_columns = df.reindex(columns=new_columns)

# Exemplo 3: Usando o método "ffill" para preencher valores ausentes após a reindexação
new_index = ["a", "b", "c", "d"]
df_ffill = df.reindex(labels=new_index, method="ffill")

# Exemplo 4: Reindexando usando o parâmetro "limit" para limitar a propagação
df_ffill_limit = df.reindex(labels=new_index, method="ffill", limit=1)

# Exemplo 5: Reindexando colunas e linhas ao mesmo tempo
new_index = ["a", "b", "d"]
new_columns = ["A", "B", "C"]
df_reindex_both = df.reindex(index=new_index, columns=new_columns, fill_value=0)

# Exemplo 6: Reindexando ao nível de um MultiIndex
multi_index = pd.MultiIndex.from_tuples([("a", 1), ("b", 2), ("c", 3)], names=["outer", "inner"])
df_multi = pd.DataFrame({"A": [10, 20, 30]}, index=multi_index)

new_multi_index = pd.MultiIndex.from_tuples([("a", 1), ("b", 2), ("c", 3), ("d", 4)], names=["outer", "inner"])
df_multi_reindexed = df_multi.reindex(new_multi_index, level="outer", fill_value=-1)

```

#### 1.4.2 Remoção de entradas de um eixo

Remoção de valores específicos em um DataFrame, como linhas ou colunas.

```python
# Método drop para remover linhas ou colunas de um DataFrame
#
# Sintaxe: df.drop(index, columns, axis)
#
# Parâmetros:
# - index: Especifica as linhas a serem removidas, pode ser uma única label ou uma lista de labels.
# - columns: Especifica as colunas a serem removidas, pode ser uma única label ou uma lista de labels.
# - axis: Define o eixo onde a operação será realizada (0 para linhas e 1 para colunas).
# Observação: O método drop retorna um novo DataFrame por padrão, a menos que 'inplace=True' seja especificado para modificar o DataFrame original.

# Exemplo 1: Removendo uma ou mais linhas por rótulo de índice
data = {"A": [1, 2, 3], "B": [4, 5, 6], "C": [7, 8, 9]}
index = ["a", "b", "c"]
df = pd.DataFrame(data, index=index) 

# Removendo a linha "b"
df_drop_row = df.drop(index="b")

# Removendo múltiplas linhas
df_drop_multiple_rows = df.drop(index=["a", "c"])

# Exemplo 2: Removendo uma ou mais colunas
# Removendo a coluna "B"
df_drop_column = df.drop(columns="B")

# Removendo múltiplas colunas
df_drop_multiple_columns = df.drop(columns=["A", "C"])

# Exemplo 3: Usando o parâmetro axis para remoção
# Removendo a linha "b" usando o parâmetro axis (equivalente a drop(index="b"))
df_drop_axis = df.drop("b", axis=0)

# Removendo a coluna "B" usando axis (equivalente a drop(columns="B"))
df_drop_column_axis = df.drop("B", axis=1)

# Exemplo 4: Usando inplace=True para modificar o DataFrame original
df_inplace = df.copy()  # Criando uma cópia para não modificar o original
df_inplace.drop(index="a", inplace=True)
```

#### 1.4.3 Indexação com loc e iloc

Utiliza rótulos (`loc`) ou inteiros (`iloc`) para selecionar dados.

Útil ao manipular uma combinação específica de linhas e colunas com condições; caso contrário, a manipulação direta é suficiente.

| **Cenário** | **Método** |
|  |  |
| Você sabe os **rótulos** de índices ou colunas | `.loc` |
| Você sabe a **posição** (inteira) dos dados | `.iloc` |
| Precisa de uma **condição lógica** | `.loc` |
| Trabalhando com **fatias incluindo os limites** | `.loc` |
| Índices ou rótulos não importam | `.iloc` |
| Dados com significado claro nos índices | `.loc` |
| Dados indexados numericamente | `.iloc` |

```python
# Métodos para acessar e manipular dados em um DataFrame Pandas
#
# Sintaxe: 
# :manipulação direta: df[column]  
# df.loc[rows]
# df.loc[:, cols]
# df.loc[rows, cols]
# df.iloc[rows]
# df.iloc[rows, cols]

# Exemplo de DataFrame
data = {"A": [10, 20, 30], "B": [40, 50, 60], "C": [70, 80, 90]}
index = ["a", "b", "c"]
df = pd.DataFrame(data, index=index)

# 1. Seleção de uma única coluna usando colchetes
# Acessa a coluna "A"

col_a = df["A"]

# 2. Seleção de uma ou mais linhas usando df.loc[rows]
# Acessa a linha "b"
row_b = df.loc["b"]

# Acessa múltiplas linhas
multiple_rows = df.loc[["a", "c"]]

# 3. Seleção de todas as linhas e colunas específicas com df.loc[:, cols]
# Acessa todas as linhas, mas apenas as colunas "A" e "B"
cols_ab = df.loc[:, ["A", "B"]]

# 4. Seleção de linhas e colunas específicas com df.loc[rows, cols]
# Acessa as linhas "a" e "b", e as colunas "A" e "C"
rows_ac = df.loc[["a", "b"], ["A", "C"]]

# 5. Seleção de linhas por posição com df.iloc[rows]
# Acessa a primeira linha (índice 0)
row_0 = df.iloc[0]

# Acessa múltiplas linhas por posição
rows_0_2 = df.iloc[[0, 2]]

# 6. Seleção de linhas e colunas por posição com df.iloc[rows, cols]
# Acessa a primeira e segunda linhas e as colunas 0 e 2 (posição)
rows_cols = df.iloc[[0, 1], [0, 2]]

# 7. Fatiamento
# Linhas por rótulo
rows_slice_loc = df.loc["a":"b"]

# Linhas e colunas por posição
rows_cols_slice_iloc = df.iloc[0:2, 0:2]

# 8. Condição lógica
# Selecionar linhas
condition_loc = df.loc[df["A"] > 15]  

# Selecionar linhas e colunas específicas
condition_columns_loc = df.loc[df["A"] > 15, ["B", "C"]]
```

#### 1.4.4 Ordenação e Classificação

Ordena os dados com base nos rótulos do índice ou colunas.

```python
# Método sort_index para ordenar um DataFrame ou Série com base nos índices (linhas ou colunas)
#
# Sintaxe: sort_index(axis, ascending=False, na_position="first")
#
# Parâmetros:
# - axis: Define o eixo de ordenação (0 para ordenar as linhas, *1 para ordenar as colunas*).
# - ascending: Se False, a ordenação será em ordem decrescente (o padrão é True, ou seja, crescente).
# - na_position: Define a posição dos valores ausentes (NaN) ao ordenar. Pode ser "first" para colocar NaNs no início ou "last" para colocá-los no final.

# Exemplo de DataFrame
data = {"A": [10, 20, 30], "B": [np.nan, 50, 60], "C": [70, np.nan, 90]}
index = ["b", "a", "c"]
df = pd.DataFrame(data, index=index)

# Exemplo 1: Ordenar linhas pelo índice em ordem crescente
df_sorted_index = df.sort_index(axis=0, ascending=True)

# Exemplo 2: Ordenar linhas pelo índice em ordem decrescente
df_sorted_index_desc = df.sort_index(axis=0, ascending=False)

# Exemplo 3: Ordenar colunas pelo nome em ordem crescente
df_sorted_columns = df.sort_index(axis=1, ascending=True)

# Exemplo 4: Ordenar colunas pelo nome em ordem decrescente
df_sorted_columns_desc = df.sort_index(axis=1, ascending=False)

# Exemplo 5: Ordenar com NaN em primeiro lugar (na_position="first")
df_sorted_nan_first = df.sort_index(axis=0, ascending=True, na_position="first")

# Exemplo 6: Ordenar com NaN em último lugar (na_position="last")
df_sorted_nan_last = df.sort_index(axis=0, ascending=True, na_position="last")
```

Ordena os dados com base nos seus valores.

```python
# Método sort_values para ordenar um DataFrame ou Series com base nos valores de uma ou mais colunas
#
# Sintaxe: sort_values(by, axis=0, ascending=True, na_position="last", inplace=False)
#
# Parâmetros:
# - by: Nome(s) da(s) coluna(s) ou rótulo(s) de índice pelos quais ordenar.
# - axis: Define o eixo de ordenação (0 para ordenar as linhas com base nos valores das colunas, 1 para ordenar as colunas com base nos valores das linhas).
# - ascending: Se True (padrão), ordena em ordem crescente; se False, em ordem decrescente.
# - na_position: Define a posição dos valores ausentes (NaN) ao ordenar. Pode ser "first" para colocar NaNs no início ou "last" para colocá-los no final.
# - inplace: Se True, a ordenação será aplicada diretamente ao DataFrame/Series original. Se False (padrão), retornará um novo DataFrame/Series ordenado.

# Exemplo de DataFrame
data = {"A": [10, 20, 30], "B": [np.nan, 50, 60], "C": [70, np.nan, 90]}
index = ["b", "a", "c"]
df = pd.DataFrame(data, index=index)

# Exemplo 1: Ordenar DataFrame pela coluna 'A' em ordem crescente
df_sorted_by_A = df.sort_values(by='A', ascending=True)

# Exemplo 2: Ordenar DataFrame pela coluna 'A' em ordem decrescente
df_sorted_by_A_desc = df.sort_values(by='A', ascending=False)

# Exemplo 3: Ordenar DataFrame por mais de uma coluna ('A' e 'B'), em ordem crescente
df_sorted_by_A_B = df.sort_values(by=['A', 'B'], ascending=True)

# Exemplo 4: Ordenar DataFrame por mais de uma coluna ('A' e 'B'), com diferentes ordens (crescente para 'A' e decrescente para 'B')
df_sorted_by_A_B_mixed = df.sort_values(by=['A', 'B'], ascending=[True, False])

# Exemplo 5: Ordenar DataFrame com NaNs em primeiro lugar (na_position="first")
df_sorted_nan_first = df.sort_values(by='A', ascending=True, na_position="first")

# Exemplo 6: Ordenar DataFrame com NaNs em último lugar (na_position="last")
df_sorted_nan_last = df.sort_values(by='A', ascending=True, na_position="last")

# Exemplo 7: Ordenar DataFrame em ordem crescente e aplicar diretamente no DataFrame original (inplace=True)
df.sort_values(by='A', ascending=True, inplace=True)
```

#### 1.4.5 Estatística Descretiva

Fornece resumos estatísticos, correlações, contagem de valores, entre outros.

```python
# Múltiplas sínteses estatísticas básicas
# Gera estatísticas descritivas para colunas numéricas e não numéricas. Múltiplas síntese estatísticas.
df.describe(include="all")  # 'include="all"' para incluir colunas numéricas, categóricas e de objetos (strings)

# Correlação entre as colunas
# Calcula a matriz de correlação entre as colunas numéricas do DataFrame
df.corr(method="pearson")  # O método 'pearson' é o padrão; outros métodos incluem 'spearman' e 'kendall'

# Covariância entre as colunas
# Calcula a covariância entre colunas numéricas do DataFrame
df.cov()

# Valores únicos de uma coluna específica ou de todo o DataFrame
# Retorna um array com os valores únicos de uma coluna específica
df["column_name"].unique()  # Substitua 'column_name' pelo nome da coluna desejada

# Contagens de valores de uma coluna específica
# Conta a frequência de valores únicos na coluna especificada
df["column_name"].value_counts(normalize=True)  # 'normalize=True' retorna a proporção, caso contrário retorna a contagem absoluta

# Verificar pertencimento de valores
# Retorna uma Série booleana indicando se os valores de uma coluna pertencem à lista fornecida
df["column_name"].isin([value1, value2, value3])  # Substitua 'column_name' pela coluna e forneça a lista de valores
```

## 2. Carregamento de dados, armazenamento e formatos de arquivos



Pandas facilita o carregamento e gravação de dados em diversos formatos como CSV, Excel, JSON, SQL, HTML, entre outros.

### **2.1 Leitura e escrita de dadsos no formato texto**

Leitura de arquivos de diferentes formatos.

```python
# Leitura
#
# Leitura de arquivos CSV
# Parâmetros:
# - path: Caminho do arquivo ou URL.
# - sep: Delimitador/Separador dos dados (padrão é ','). Pode ser ';', '\t', etc.
# - names: Lista de nomes de colunas a ser usada (se o arquivo não tiver cabeçalhos).
# - index_col: Coluna que será usada como índice do DataFrame.
df_csv = pd.read_csv(path="data.csv", sep=",", names=None, index_col=None)

# Leitura de arquivos Excel
# - sheet_name: Nome ou número da planilha (padrão é a primeira planilha).
df_excel = pd.read_excel("data.xlsx", sheet_name="Sheet1")

# Leitura de arquivos JSON
# - orient: Define o formato do JSON (por exemplo: 'records', 'split', 'index').
df_json = pd.read_json("data.json")

# Leitura de dados de um banco de dados SQL
# - sql: A consulta SQL.
# - con: Objeto de conexão com o banco de dados.
conn = sqlite3.connect("database.db")
df_sql = pd.read_sql("SELECT * FROM table_name", con=conn)

# Leitura de arquivos XML
df_xml = pd.read_xml("data.xml")

# Leitura de tabelas HTML
# Retorna uma lista de DataFrames, já que uma página HTML pode conter várias tabelas.
df_html = pd.read_html("https://example.com/tables.html")[0]  # Acessa a primeira tabela

```

```python
# Gravação
#
# Gravação de DataFrame em um arquivo CSV
# Parâmetros:
# - path: Caminho onde o arquivo será salvo.
# - sep: Define o separador (padrão é ',').
# - index: Se True, grava os índices do DataFrame (padrão é True).
data.to_csv("output.csv", sep=",", index=True)

# Gravação de DataFrame em um arquivo Excel
# - sheet_name: Nome da planilha onde os dados serão gravados.
data.to_excel("output.xlsx", sheet_name="Sheet1", index=False)

# Gravação de DataFrame em um arquivo JSON
# - orient: Define o formato do JSON (ex: 'records', 'index').
data.to_json("output.json", orient="records")

# Gravação de DataFrame em um banco de dados SQL
# - name: Nome da tabela.
# - con: Conexão com o banco de dados.
data.to_sql("table_name", con=conn, if_exists="replace", index=False)  # 'replace' para sobrescrever a tabela

# Gravação de DataFrame em um arquivo XML
data.to_xml("output.xml", index=False)

# Gravação de DataFrame em um arquivo HTML
data.to_html("output.html", index=False)

```

### **2.2 Interações**

#### 2.2.1 Web APIs

Requisições HTTP e conversão de dados para DataFrames.

```python
# Web APIs
#
# Importando biblioteca 'request'
import requests

# Fazendo a requisição HTTP para a API do GitHub
url = "http://api.github.com/repos/pandas-dev/pandas/issues"
resp = requests.get(url)
resp.raise_for_status()  # Verifica se houve erro na requisição

# Convertendo a resposta em JSON
data = resp.json()

# Exibindo o título do primeiro issue para visualização
print("Título do primeiro issue:", data[0]["title"])

# Criando o DataFrame a partir dos dados obtidos
# Filtrando as colunas "number", "title", "labels", "state"
issues = pd.DataFrame(data, columns=["number", "title", "labels", "state"])

# Exibindo as primeiras linhas do DataFrame
print(issues.head())

```

#### 2.2.2 Banco de dados

Conexão com bancos de dados SQL via SQLAlchemy ou Psycopg2.

```python
# SQLAlchemy
#
# Importando bibliotecas necessárias
import sqlite3
import sqlalchemy as sqla

# Definindo a consulta SQL para criar uma tabela chamada 'test'
query = """
CREATE TABLE IF NOT EXISTS test (
    a VARCHAR(20),
    b VARCHAR(20),
    c REAL,
    d INTEGER
);"""

# Conectando ao banco de dados SQLite, criando o arquivo 'mydata.sqlite' se não existir
con = sqlite3.connect("mydata.sqlite")

# Executando a consulta de criação da tabela no banco de dados
con.execute(query)

# Confirmando as alterações (commit) para garantir que a tabela seja criada no banco de dados
con.commit()

# Fechando a conexão SQLite para seguir com SQLAlchemy
con.close()

# Criando uma engine SQLAlchemy para se conectar ao banco de dados SQLite
engine = sqla.create_engine("sqlite:///mydata.sqlite")

# Inserindo alguns dados na tabela 'test' para demonstração
insert_query = """
INSERT INTO test (a, b, c, d) VALUES
('John', 'Doe', 1.5, 25),
('Jane', 'Doe', 2.7, 30),
('Alice', 'Smith', 3.8, 22);
"""

# Executando a inserção de dados usando a engine
with engine.connect() as connection:
    connection.execute(insert_query)

# Lendo os dados da tabela 'test' e retornando como um DataFrame do Pandas
df = pd.read_sql("SELECT * FROM test", engine)

# Exibindo os dados lidos
print(df)

# Fechando a engine (SQLAlchemy cuida automaticamente, mas é uma boa prática)
engine.dispose()
```

```python
# PsygoPG2
#
# Importando bibliotecas 'psycopg2'
import psycopg2

# Conectando ao banco de dados PostgreSQL
conn = psycopg2.connect(
    dbname="nome_do_banco",    # Substitua pelo nome do banco de dados
    user="usuario",            # Substitua pelo nome do usuário
    password="senha",          # Substitua pela senha
    host="localhost",          # Substitua pelo endereço do host (ex: 'localhost' ou IP do servidor)
    port="5432"                # Substitua pela porta do PostgreSQL (padrão: 5432)
)

# Criando um cursor para executar consultas SQL
cursor = conn.cursor()

# Definindo a consulta SQL para selecionar os dados da tabela
query = "SELECT * FROM nome_da_tabela"  # Substitua pelo nome da tabela

# Usando pandas para ler o resultado da consulta diretamente em um DataFrame
df = pd.read_sql(query, conn)

# Exibindo as primeiras linhas do DataFrame
print(df.head())

# Fechando o cursor e a conexão com o banco de dados
cursor.close()
conn.close()
```

## 3. Limpeza e preparação dos dados



Carregamento, limpeza, transformação e reorganização = tratar dados ausentes, dados duplicados, manipulação de strings e entre outras transformações de dados.

### **3.1 Manipulação de dados ausentes**

Dados ausentes de NA (Not Available); Identificação de problemas de coleta ou das distorções que eles possam causar.

```python
# Removendo valores NA (nulos) do DataFrame
#
# Sintaxe: df.dropna(how, thresh)
#
# Parâmetros:
# - how: Define se a remoção ocorre quando "any" valor na linha ou coluna for NA, ou "all" se todos os valores forem NA.
# - thresh: Define um número mínimo de valores não-NA necessários para a linha/coluna não ser removida.

# Exemplo: Remove linhas onde qualquer valor é NA
df.dropna(how="any")

# Exemplo: Remove linhas onde todos os valores são NA
df.dropna(how="all") # df.dropna()

# Exemplo: Mantém apenas as linhas com pelo menos 3 valores não-NA
df.dropna(thresh=3)
```

```python
# Preenche valores NA com um valor específico ou utilizando um método de preenchimento
#
# Sintaxe: df.fillna(value, method, aixs, limit)
#
# Parâmetros:
# - value: O valor com o qual preencher os valores NA (pode ser um valor escalar ou um dicionário).
# - method: Método de preenchimento, como "ffill" (preenche com o valor anterior) ou "bfill" (preenche com o próximo valor).
# - axis: Define se o preenchimento é por linhas (axis=0) ou colunas (axis=1).
# - limit: Limita o número de valores consecutivos preenchidos.

# Exemplo 1: Preenche todos os valores NA com 0
df.fillna(value=0)

# Exemplo 2: Preenche valores NA com o valor anterior na mesma coluna
df.fillna(method="ffill", axis=0)

# Exemplo 3: Preenche valores NA com o valor seguinte na mesma linha, limitado a uma substituição por vez
df.fillna(method="bfill", axis=1, limit=1)

# Verificando se existem valores NA (nulos) no DataFrame
# Retorna um DataFrame booleano, onde True indica a presença de NA
df.isna()

# Exemplo 4: Exibe as posições dos valores NA no DataFrame
print(df.isna())

# Verificando a ausência de valores NA (nulos)
# Retorna um DataFrame booleano, onde True indica que o valor NÃO é NA
df.notna()

# Exemplo 5: Exibe as posições onde os valores NÃO são NA
print(df.notna())
```

**Filtagram de dados ausentes**
Utilizar o método `dropna` para remover qualquer linha que contenha um valor ausente. Esse método retornam novos objetos por padrão e não modificam o conteúdo do objeto original.

**Preenchendo dados ausentes**
Em vez de filtrar os dados, podemos substituir/preencher com outro valor de interesse.

`fillna` com um dicionário; Selecionar o ultimo valor antes do NA e copia para os seguintes com `method="ffill"`; Usando mediana ou a média estatística.

### **3.2 Transformação de dados**

Remoção de duplicatas, substituição de valores e Detecção e filtragem de valores discrepantes (outliers).

```python
# Remoção de linhas duplicadas no DataFrame
#
# Sintaxe: df.drop_duplicates()
#
# Parâmetros:
# - subset: Especifica as colunas que devem ser consideradas para identificar duplicatas.
# - keep: Define qual duplicata manter ("first", "last", ou False para remover todas).
# - inplace: Se True, modifica o DataFrame original.

# Exemplo: Remove duplicatas com base em todas as colunas, mantendo a primeira ocorrência
df.drop_duplicates()

# Exemplo: Remove duplicatas com base em uma coluna específica
df.drop_duplicates(subset="column_name")

# Exemplo: Remove todas as duplicatas (não mantém nenhuma ocorrência)
df.drop_duplicates(keep=False)
```

```python
# Substituição de valores no DataFrame
#
# Sintaxe: df.replace()
#
# Parâmetros:
# - to_replace: O valor ou lista de valores a ser substituído.
# - value: O novo valor com o qual substituir.
# - inplace: Se True, modifica o DataFrame original.

# Exemplo: Substituir todos os valores 0 por NaN
df.replace(to_replace=0, value=np.nan)

# Exemplo: Substituir múltiplos valores por diferentes valores
df.replace({0: np.nan, -1: 0})

# Exemplo: Substituir valores de uma coluna específica
df["column_name"].replace("old_value", "new_value")

```

```python
# Resumo estatístico das colunas do DataFrame (para ajudar na identificação de outliers)
# df.describe() fornece métricas como média, desvio padrão, e quartis
df.describe()

# Exemplo: Detecção de outliers com base no desvio padrão (considerando valores que estão além de 3 desvios padrão)
# value pode ser o DataFrame ou uma coluna específica
# .abs() pega o valor absoluto (desconsiderando o sinal) e .any(axis='columns') verifica se qualquer valor na linha é discrepante
outliers = df[(np.abs(df - df.mean()) > (3 * df.std())).any(axis="columns")]

# Exemplo: Visualizando os outliers
print(outliers)

# Uso de np.sign() para verificar a direção do desvio
# Exemplo: Adicionando uma coluna com a direção do desvio (1 ou -1 para valores discrepantes)
df["outlier_sign"] = np.sign(df - df.mean())
print(df["outlier_sign"])

```

### **3.2 Manipulação de string**

Funções de manipulação de strings, como dividir, juntar, e verificar padrões.

```python
# Contar ocorrências de uma substring
count()

# Verificar se a string termina ou começa com um prefixo/sufixo
endswith(), startswith()

# Juntar uma lista de strings em uma única string
join()

# Encontrar o índice da primeira ocorrência de uma substring
index()

# Encontrar a primeira ocorrência de uma substring
find()

# Encontrar a última ocorrência de uma substring
rfind()

# Substituir uma substring por outra
replace()

# Remover espaços em branco
strip(), rstrip(), lstrip()

# Dividir a string em uma lista de substrings
split()

# Converter a string para minúsculas e maiúsculas
lower(), upper()

# Normalizar a string (case folding)
casefold()

# Ajustar a string à esquerda ou à direita
ljust(), rjust()

# Encontra todas as ocorrências de uma substring (com regex)
findall()

# Obtém um valor de um dicionário
get()

# Verifica se a string contém apenas caracteres alfanuméricos
isalnum()

# Verifica se a string contém apenas letras ou é numérica
isalpha(), isnumeric()

# Verifica se a string contém apenas dígitos decimais
isdecimal()

# Verifica se a string contém apenas dígitos
isdigit()

# Verifica se a string está em minúsculas ou maiúsculas
islower(), isupper()
```

## 4. Junção, Combinação e Reformatação



Dados podem estar espalhados em vários arquivos ou banco de dados ou organizados em formato que não seja apropriado para análise

### **4.1 Indexação Hierárquica**

Permite a criação de vários níveis de índices (MultiIndex), possibilitando uma organização complexa de dados.

```python
# 1. Criando uma Series com MultiIndex
data = pd.Series([10, 20, 30], index=[["a", "b", "c"], [1, 2, 3]])

# Exibindo o MultiIndex da Series
data.index

# 2. Indexação Parcial
# Acessando um nível específico do MultiIndex
# Exemplo: Acessando todos os valores do índice "b"
data["b"]

# Indexação parcial por fatia de rótulos
# Exemplo: Acessando valores entre os índices "a" e "b"
data["a":"b"]

# Utilizando loc para seleção de múltiplos rótulos
# Exemplo: Acessando valores dos índices "b" e "c"
data.loc[["b", "c"]]

# 3. Reformatação da Tabela Dinâmica ('unstack' e 'stack')
# Reformatação da Series para um DataFrame com `unstack`
# Transforma o segundo nível do índice em colunas
data.unstack()

# Voltando ao formato original com `stack`
# Transforma o DataFrame de volta para uma Series
unstacked.stack()

# 4. Verifica quantos níveis o MultiIndex possui
data.index.nlevels  

# 5. Reorganização e Ordenação de Níveis
# Troca os níveis do MultiIndex (sem alterar os dados)
data.swaplevel()

# Ordena o MultiIndex com base em um nível específico
# Exemplo: Ordenando pelo segundo nível do índice (os valores 1, 2, 3)
sorted_data = data.sort_index(level=1)

# 6. Indexação com Colunas
# Criando um DataFrame com MultiIndex nas colunas usando 'set_index'
df = pd.DataFrame({
    "d": ["X", "Y", "Z"],
    "e": ["W", "Q", "T"],
    "values": [10, 20, 30]
})

# Definindo "d" e "e" como índices, sem remover as colunas originais ('drop=False')
df.set_index(["d", "e"], drop=False)
```

### **4.2 Agrupamento de Dados**

O método `groupby` agrupa dados com base em uma ou mais colunas, permitindo realizar operações de agregação, transformação e filtragem em grupos específicos.

Sequência de etapas principais: dividir (split), aplicar (apply) e combinar (combine).

```python
# Parâmetros
df.groupby(
    by=None,             # Coluna(s) ou índice(s) pelos quais os dados serão agrupados
    axis=0,              # Eixo para agrupar (0 para linhas, 1 para colunas, padrão é 0)
    level=None,          # Se o DataFrame tiver MultiIndex, agrupa por nível específico
    as_index=True,       # Se True (padrão), os grupos se tornam índices no resultado
    sort=True,           # Ordena os grupos por seus valores (padrão é True)
    group_keys=True,     # Adiciona a chave de grupo aos índices (padrão é True)
    squeeze=False,       # Se True, reduz a dimensionalidade se possível (padrão é False)
    observed=False,      # Para categorias, inclui apenas categorias observadas (padrão é False)
    dropna=True          # Exclui valores NaN no agrupamento (padrão é True)
)

# Operações Comuns
# Exemplo 1: Soma dos valores por categoria
# Agrupa os dados pela coluna "categoria" e calcula a soma dos valores na coluna "valor"
df.groupby("categoria")["valor"].sum()

# Exemplo 2: Múltiplas funções de agregação (soma, média, contagem)
# Agrupa pela coluna "categoria" e calcula as funções "sum", "mean", e "count" na coluna "valor"
df.groupby("categoria")["valor"].agg(["sum", "mean", "count"])

# Exemplo 3: Agrupamento por múltiplas colunas
# Agrupa pelas colunas "coluna1" e "coluna2" e calcula a média dos valores na coluna "valor"
df.groupby(["coluna1", "coluna2"])["valor"].mean()

# Transformação de Dados
# Exemplo: Normalização dos valores dentro de cada grupo
# Normaliza a coluna "valor" dentro de cada grupo da coluna "categoria" com média 0 e desvio padrão 1
df["normalizado"] = df.groupby("categoria")["valor"].transform(lambda x: (x - x.mean()) / x.std())

# Filtragem de Grupos
# Exemplo: Filtragem de grupos com base em uma condição
# Filtra os grupos onde a média da coluna "valor" dentro da "categoria" é maior que 10
filtered_df = df.groupby("categoria").filter(lambda x: x["valor"].mean() > 10)

# Aplicação de Funções Personalizadas
# Exemplo: Aplicação de função personalizada a cada grupo
# Ordena os valores dentro de cada grupo da coluna "categoria" pela coluna "valor", de forma decrescente
df.groupby("categoria").apply(lambda x: x.sort_values(by="valor", ascending=False))
```

### **4.3 Combinação e mesclagem de conjutnos de dados**

Mesclagem (merge) ou junção: combina conjuntos de dados associando linhas com o uso de uma ou mais chaves

```python
# Parâmetros
pd.merge(
    left,                  # DataFrame à esquerda
    right,                 # DataFrame à direita
    how="inner",           # Tipo de junção: 'left', 'right', 'outer', 'inner' (padrão é 'inner')
    on=None,               # Coluna ou colunas comuns para junção em ambos os DataFrames
    left_on=None,          # Coluna ou colunas do DataFrame à esquerda para junção
    right_on=None,         # Coluna ou colunas do DataFrame à direita para junção
    left_index=False,      # Usa os índices do DataFrame à esquerda para junção
    right_index=False,     # Usa os índices do DataFrame à direita para junção
    sort=True,             # Ordena as colunas de junção após a fusão (padrão é True)
    suffixes=("_x", "_y"), # Sufixos para colunas sobrepostas
    copy=True,             # Faz uma cópia dos dados (padrão é True)
    indicator=False,       # Adiciona coluna indicando a origem de cada linha
    validate=None          # Valida o tipo de junção ('one_to_one', 'one_to_many', 'many_to_one', 'many_to_many')
)

# Exemplo 1: Junção simples com colunas comuns
pd.merge(df1, df2, how="inner", on="id")

# Exemplo 2: Junção com colunas diferentes
pd.merge(df1, df2, how="left", left_on="id_left", right_on="id_right")
# Exemplo 3: Junção com índices
pd.merge(df1, df2, how="right", left_index=True, right_index=True)

# Exemplo 4: Junção com indicador de origem das linhas
pd.merge(df1, df2, how="outer", on="id", indicator=True)

# Exemplo 5: Validação do tipo de junção
pd.merge(df1, df2, how="inner", on="id", validate="one_to_many")
```

#### 4.3.1 Concatenaçao ao longo de um eixo

Concatena DataFrames ao longo de um eixo (linhas ou colunas).

```python
# Parâmetros
pd.concat(
    objs,                    # Lista ou dicionário de DataFrames/Series para concatenar
    axis=0,                  # Eixo para concatenar ao longo: 0 para linhas, 1 para colunas (padrão é 0)
    join='outer',            # Tipo de junção: 'inner' ou 'outer' (padrão é 'outer')
    ignore_index=False,      # Ignora os índices existentes e cria novos (padrão é False)
    keys=None,               # Chaves para associar aos DataFrames/Series resultantes
    levels=None,             # Níveis específicos para MultiIndex, se fornecido
    names=None,                # Nomes para os níveis do índice resultante
    verify_integrity=False, # Verifica a integridade da concatenação (padrão é False)
    sort=False,              # Ordena eixos não concatenados se necessário (padrão é False)
    copy=True                # Copia os dados, em vez de fazer referência direta (padrão é True)
)

# Exmeplo 1: df1 e df2 ao longo das linhas (axis=0, padrão)
pd.concat([df1, df2])

# Exmeplo 2: df1 e df2 ao longo das colunas (axis=1)
pd.concat([df1, df2], axis=1)

# Exmeplo 3: df1 e df2 com novos índices, ignorando os originais
pd.concat([df1, df2], ignore_index=True)

# Exmeplo 4: df1 e df3 apenas nas colunas comuns (A), usando join='inner'
pd.concat([df1, df3], join="inner")

# Exmeplo 5: df1 e df2 com chaves, criando um MultiIndex
pd.concat([df1, df2], keys=["df1", "df2"])

# Exemplo 6: Verifica se há duplicatas nos índices após a concatenação
pd.concat([df1, df2], verify_integrity=True)
    
# Exemplo 7: df1 e df2 com índices totalmente ou parcialmente sobrepostos
# Método 'combine_first'
df1.combine_first(df2)
```

### **4.4 Reformatação e pivotamento**

#### 4.4.1 Reformatação

A reformatação, também conhecida como "melting", transforma um DataFrame de um formato "largo" para um formato "longo". Isso é útil quando queremos transformar colunas em valores para facilitar agregações ou comparações.

```python
# Parâmetros
pd.melt(
    frame,                # DataFrame que será reformado
    id_vars=None,         # Colunas a manter (não derreter)
    value_vars=None,      # Colunas a derreter (transformar em valores)
    var_name=None,        # Nome da nova coluna de variáveis
    value_name="value",   # Nome da nova coluna de valores
    col_level=None,       # Nível de coluna a derreter se houver MultiIndex
    ignore_index=True     # Ignorar o índice original ou não (padrão é True)
)

# DataFrame original
df = pd.DataFrame({
    "Nome": ["Ana", "Beto", "Carla"],
    "Idade": [23, 45, 30],
    "Altura": [1.65, 1.80, 1.70],
    "Peso": [55, 85, 68]
})

# Exemplo 1: Derretendo o DataFrame
pd.melt(df, id_vars=["Nome"], value_vars=["Altura", "Peso"], var_name="Medida", value_name="Valor")

# Exemplo 2: Derretendo todas as colunas, exceto "Nome"
pd.melt(df, id_vars="Nome")

# Exemplo 3: Derretendo o DataFrame, mas mantendo o índice original
pd.melt(df, id_vars=["Nome"], value_vars=["Altura", "Peso"], ignore_index=False)
```

#### 4.4.2 Pivotamento

O pivotamento faz o oposto do "melt", transformando dados de formato "longo" para "largo". Ele reorganiza os dados para que valores de uma coluna se tornem colunas, com base em outra variável.

```python
# Parâmetros
df.pivot(
    index=None,           # Coluna(s) para usar como índice
    columns=None,         # Coluna(s) cujos valores se tornarão colunas
    values=None           # Coluna(s) cujos valores serão os valores resultantes
)

# DataFrame
df = pd.DataFrame({
    "Nome": ["Ana", "Beto", "Carla", "Ana", "Beto", "Carla"],
    "Ano": [2020, 2020, 2020, 2021, 2021, 2021],
    "Vendas": [500, 600, 700, 800, 900, 1000]
})

# Exemplo 1: Pivotar um DataFrame simples
df.pivot(index="Nome", columns="Ano", values="Vendas")

# Exemplo 2: Pivotar com múltiplos índices
df.pivot(index=["Nome", "Produto"], columns="Ano", values="Vendas")
 
# Exemplo 3: Pivot sem especificar values (mantém todas as colunas)
df.pivot(index="Nome", columns="Ano")
```

A função pivot_table permite agregar dados, o que não é possível com pivot simples. Ela oferece mais flexibilidade, permitindo calcular médias, somas e outros métodos de agregação.

```python
# Parâmetros
pd.pivot_table(
    data,                # DataFrame
    values=None,         # Coluna(s) cujos valores serão agregados
    index=None,          # Coluna(s) para usar como índice
    columns=None,        # Coluna(s) cujos valores se tornarão colunas
    aggfunc='mean',      # Função de agregação (padrão é 'mean')
    fill_value=None,     # Valor para preencher dados ausentes
    margins=False,       # Adiciona totais nas margens (padrão é False)
    dropna=True,         # Remove colunas com todos valores NaN
    margins_name='All'   # Nome da linha/coluna de total
)

# DataFrame
df = pd.DataFrame({
    "Nome": ["Ana", "Beto", "Carla", "Ana", "Beto", "Carla"],
    "Ano": [2020, 2020, 2020, 2021, 2021, 2021],
    "Vendas": [500, 600, 700, 800, 900, 1000]
})

# Exemplo 1: Tabela dinâmica simples
# Criando uma tabela dinâmica (pivot table)
pd.pivot_table(df, values="Vendas", index="Nome", columns="Ano", aggfunc="sum")

# Exemplo 2: Tabela dinâmica com múltiplas funções de agregação
# Criando uma tabela dinâmica com várias funções de agregação
pd.pivot_table(df, values="Vendas", index="Nome", columns="Ano", aggfunc=["sum", "mean"])

# Exemplo 3: Preenchendo valores ausentes com fill_value
# Adicionando valores faltantes ao DataFrame
df.loc[6] = ["Ana", 2022, None]

# Criando uma tabela dinâmica e preenchendo valores ausentes com 0
pd.pivot_table(df, values="Vendas", index="Nome", columns="Ano", aggfunc="sum", fill_value=0)

# Exemplo 4: Adicionando totais marginais com margins
# Criando uma tabela dinâmica com totais marginais
pd.pivot_table(df, values="Vendas", index="Nome", columns="Ano", aggfunc="sum", margins=True, margins_name="Total")

# Exemplo 5: Usando múltiplos índices e colunas
pd.pivot_table(df, values="Vendas", index=["Nome", "Produto"], columns="Ano", aggfunc="sum")
```
