# PANDAS
---

## Índice

1. **Introdução ao pandas**
   - [1.1 Séries](#11-séries)
   - [1.2 DataFrame](#12-dataframe)
   - [1.3 Objetos Index](#13-objetos-index)
   - [1.4 Funcionalidades essenciais](#14-funcionalidades-essenciais)
     - [1.4.1 Reindexação](#141-reindexação)
     - [1.4.2 Remoção de entradas de um eixo](#142-remoção-de-entradas-de-um-eixo)
     - [1.4.3 Indexação com loc e iloc](#143-indexação-com-loc-e-iloc)
     - [1.4.4 Ordenação e classificação](#144-ordenação-e-classificação)
     - [1.4.5 Estatística descritiva](#145-estatística-descritiva)

2. **Carregamento de dados, armazenamento e formatos de arquivos**
   - [2.1 Leitura e escrita de dados no formato texto](#21-leitura-e-escrita-de-dados-no-formato-texto)
   - [2.2 Interações](#22-interações)
     - [2.2.1 APIs Web](#221-apis-web)
     - [2.2.2 Banco de dados](#222-banco-de-dados)

3. **Limpeza e preparação dos dados**
   - [3.1 Manipulação de dados ausentes](#31-manipulação-de-dados-ausentes)
   - [3.2 Transformação de dados](#32-transformação-de-dados)
   - [3.3 Manipulação de strings](#33-manipulação-de-strings)

4. **Junção, combinação e reformatação**
   - [4.1 Indexação hierárquica](#41-indexação-hierárquica)
   - [4.2 Agrupamento de dados](#42-agrupamento-de-dados)
   - [4.3 Combinação e mesclagem de conjuntos de dados](#43-combinação-e-mesclagem-de-conjuntos-de-dados)
     - [4.3.1 Concatenação ao longo de um eixo](#431-concatenação-ao-longo-de-um-eixo)
   - [4.4 Reformatação e pivotamento](#44-reformatação-e-pivotamento)
     - [4.4.1 Reformatação](#441-reformatação)
     - [4.4.2 Pivotamento](#442-pivotamento)


## 1. Introdução ao pandas
O pandas é uma biblioteca poderosa para manipulação e análise de dados em Python. Ele oferece estruturas de dados flexíveis, como `Series` e `DataFrame`, que permitem trabalhar com dados de forma eficiente.

### **1.1 Séries**
Uma `Series` é uma sequência unidimensional de valores (semelhante a um array) com rótulos chamados de índice. 

```python
pd.Series(data=None, index=None, dtype=None, name=None, copy=None, fastpath=<no_default>)
```

### **1.2 DataFrame**
O `DataFrame` é uma tabela bidimensional com colunas nomeadas e indexadas. Ele pode ser visto como um dicionário de `Series` alinhadas. Cada coluna pode conter tipos de dados diferentes.

```python
pd.DataFrame(data=None, index=None, columns=None, dtype=None, copy=None)
```

### **1.3 Objetos Index**
Um `Index` contém os rótulos dos eixos e outros metadados. Eles são imutáveis e usados para alinhar dados.

```python
pd.Index(data=None, dtype=None, copy=False, name=None, tupleize_cols=True)
```

### **1.4 Funcionalidade essencias**
#### 1.4.1 Reindexação
Cria um novo objeto com os valores reorganizados para ficarem alinhados com o novo índice. Pode alterar o índice das linhas, colunas, ou ambos.

```python
reindex(labels, index, columns, axis, method, fill_value, limit, tolerance, level, copy)
```

#### 1.4.2 Remoção de entradas de um eixo
Remoção de valores específicos em um DataFrame, como linhas ou colunas.

```python
df.drop(index, columns, axis)
```

#### 1.4.3 Indexação com loc e iloc
Utiliza rótulos (`loc`) ou inteiros (`iloc`) para selecionar dados.

```python
df[column]
df.loc[rows]
df.loc[:, cols]
df.loc[rows, cols]
df.iloc[rows]
df.iloc[rows, cols]
df.at[row, col]
df.iat[row, col]
reindex()
```

#### 1.4.4 Ordenação e Classificação
Ordena os dados com base nos rótulos do índice ou colunas.

```python
sort_index(axis, ascending=False, na_position="first")
```

#### 1.4.5 Estatística Descretiva
Fornece resumos estatísticos, correlações, contagem de valores, entre outros.

```python
# Múltiplas síntese estatísticas
df.describe()

# Correlação e Covariância
df.corr()
df.cov()

# Valores únicos
unique()

# Contagens de valores 
value_counts()

# Pertencimento
isin()
```

## 2. Carregamento de dados, armazenamento e formatos de arquivos
Pandas facilita o carregamento e gravação de dados em diversos formatos como CSV, Excel, JSON, SQL, HTML, entre outros.

### **2.1 Leitura e escrita de dadsos no formato texto**
Leitura de arquivos de diferentes formatos.

```python
pd.read_csv(path, sep, names, index_col)
pd.read_excel()
pd.read_json()
pd.read_sql()
pd.read_xml()
pd.read_html()

# Gravação
data.to_csv(path)
data.to_excel(path)
data.to_json(path)
data.to_sql(path)
data.to_xml(path)
data.to_html(path)
```

### **2.2 Interações**
#### 2.2.1 APIs Web
Requisições HTTP e conversão de dados para DataFrames.

```python
import requests  

# Fazendo a requisição HTTP para a API do GitHub
url = "http://api.github.com/repos/pandas-dev/pandas/issues"
resp = requests.get(url)  
resp.raise_for_status()  # Verifica se houve erro na requisição

# Convertendo a resposta em JSON
data = resp.json()

# Visualizando o título do primeiro issue
data[0]["title"]

# Criando o DataFrame a partir dos dados obtidos
issues = pd.DataFrame(data, columns=["number", "title", "labels", "state"])

# Exibindo as primeiras linhas do DataFrame
issues.head()
```

#### 2.2.2 Banco de dados
Conexão com bancos de dados SQL via SQLAlchemy ou Psycopg2.

```python
# SQLAlchemy
import sqlite3
import sqlalchemy as sqla

# Definindo a consulta SQL para criar uma tabela chamada 'test'
query = """
CREATE TABLE test
(a VARCHAR(20), b VARCHAR(20),   
 c REAL,                        
 d INTEGER                      
);"""

# Conectando ao banco de dados SQLite, criando o arquivo 'mydata.sqlite' se não existir
con = sqlite3.connect("mydata.sqlite")

# Executando a consulta de criação da tabela no banco de dados
con.execute(query)

# Confirmando as alterações (commit) para garantir que a tabela seja criada no banco de dados
con.commit()

# Criando uma engine SQLAlchemy para se conectar ao banco de dados SQLite
db = sqla.create_engine("sqlite:///mydata.sqlite")

# Lendo os dados da tabela 'test' e retornando como um DataFrame do Pandas
pd.read_sql("SELECT * FROM test", db)

# Fechando a conexão (opcional, pois SQLAlchemy cuida disso)
engine.dispose()
```

```python
# PsygoPG2
import psycopg2

# Conectando ao banco de dados PostgreSQL
conn = psycopg2.connect(
    dbname="nome_do_banco",
    user="usuario",
    password="senha",
    host="localhost",
    port="5432"
)

# Criando um cursor
cursor = conn.cursor()

# Lendo dados do banco de dados para um DataFrame
query = "SELECT * FROM nome_da_tabela"
df = pd.read_sql(query, conn)

# Exibindo o DataFrame
print(df.head())

# Fechando a conexão
cursor.close()
conn.close()
```

## 3. Limpeza e preparação dos dados
Carregamento, limpeza, transformação e reorganização = Limpeza de dados envolve tratar dados ausentes, dados duplicados, manipulação de strings e entre outras transformações de dados.

### **3.1 Manipulação de dados ausentes**
Dados ausentes de NA (Not Available); Identificação de problemas de coleta ou das distorções que eles possam causar

```python
# Remove valores NA
df.dropna(how, thresh)

# Preenche os NA com algum valor
df.fillna(value, method, aixs, limit)

# Retorna valores bool que indica NA
df.isna()

# Negaçao de `isna`, 
df.notna()
```

**Filtagram de dados ausentes**
Utilizar o método `dropna` para remover qualquer linha que contenha um valor ausente. Esse método retornam novos objetos por padrão e não modificam o conteúdo do objeto original.

**Preenchendo dados ausentes**
Em vez de filtrar os dados, podemos substituir/preencher com outro valor de interesse.

`fillna` com um dicionário; Selecionar o ultimo valor antes do NA e copia para os seguintes com `method="ffill"`; Usando mediana ou a média estatística.

### **3.2 Transformação de dados**
Remoção de duplicatas e substituição de valores.

```python
# Remoção de duplicidades
df.drop_duplicates()

# Substituição de valores
df.replace()

# Detecção e filtragem de valors discrepantes
df.describe()
df[(value.abs() > 3).any(axis="columns")]
np.sign()
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

# Verifica se a string contém apenas letras
isalpha()

# Verifica se a string contém apenas dígitos decimais
isdecimal()

# Verifica se a string contém apenas dígitos
isdigit()

# Verifica se a string está em minúsculas
islower()

# Verifica se a string é numérica
isnumeric()

# Verifica se a string está em maiúsculas
isupper()
```

## 4. Junção, Combinação e Reformatação
Dados podem estar espalhados em vários arquivos ou banco de ddados ou organizados em formato que não seja apropriado para análise

### **4.1 Indexação Hierárquica**
Permite a criação de vários níveis de índices (MultiIndex), possibilitando uma organização complexa de dados.

```python
data = pd.Series(index=[["a", "b", "c"], [1, 2, 3]])

# MultiIndex
data.index

# Indexação parcial
data["b"]
data["a" : "b"]
data.loc[["b", "c"]]

# Reformatação da tabala dinâmica
data.unstack()
data.stack()

# Ver quantos niveis
data.index.nlevels

# Reorganização e ordenação de níveis
## Níveis trocados
data.swaplevel()

## Ordena todos os níveis do índice
data.sort_index(level=1)

# Indexação com as colunas 
data.set_index(["d", "e"], drop=False)
```

### **4.2 Agrupamento de Dados**
O método `groupby` agrupa dados com base em uma ou mais colunas, permitindo realizar operações de agregação, transformação e filtragem em grupos específicos.

Sequência de etapas principais: dividir (split), aplicar (apply) e combinar (combine).

```python
df.groupby(
    by=None,             # Coluna(s) ou índice(s) pelos quais os dados serão agrupados
    axis=0,              # Eixo para agrupar (0 para linhas, 1 para colunas, padrão é 0)
    level=None,          # Se o DataFrame tiver MultiIndex, agrupa por nível específico
    as_index=True,       # Se True (padrão), os grupos se tornam índices no resultado
    sort=True,           # Ordena os grupos por seus valores (padrão é True)
    group_keys=True,     # Adiciona a chave de grupo aos índices (padrão é True)
    squeeze=False,       # Se True, reduz dimensionalidade se possível (padrão é False)
    observed=False,      # Para categorias, inclui apenas categorias observadas (padrão é False)
    dropna=True          # Exclui valores NaN no agrupamento (padrão é True)
)

# Operações Comuns: `sum()`, `mean()`, `count()`, `min()` e `max()`
df.groupby('categoria')['valor'].sum()

# Agregação com Múltiplas Funções
df.groupby('categoria')['valor'].agg(['sum', 'mean', 'count'])

# Agrupamento por Múltiplas Colunas
df.groupby(['coluna1', 'coluna2'])['valor'].mean()

# Transformação de Dados 
df['normalizado'] = df.groupby('categoria')['valor'].transform(lambda x: (x - x.mean()) / x.std())

# Filtragem de Grupos
df.groupby('categoria').filter(lambda x: x['valor'].mean() > 10)

# Aplicação de Funções Personalizadas
df.groupby('categoria').apply(lambda x: x.sort_values(by='valor', ascending=False))
```


### **4.3 Combinação e mesclagem de conjutnos de dados**
Mesclagem (merge) ou junção: combina conjuntos de dados associando linhas com o uso de uma ou mais chaves

```python
pd.merge(df1, df2, *args)

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
    suffixes=('_x', '_y'), # Sufixos para colunas sobrepostas
    copy=True,             # Faz uma cópia dos dados (padrão é True)
    indicator=False,       # Adiciona coluna indicando a origem de cada linha
    validate=None          # Valida o tipo de junção ('one_to_one', 'one_to_many', 'many_to_one', 'many_to_many')
)
```

#### 4.3.1 Concatenaçao ao longo de um eixo
Concatena DataFrames ao longo de um eixo (linhas ou colunas).

```python
pd.concat(
    objs,                	# Lista ou dicionário de DataFrames/Series para concatenar
    axis=0,              	# Eixo para concatenar ao longo: 0 para linhas, 1 para colunas (padrão é 0)
    join='outer',        	# Tipo de junção: 'inner' ou 'outer' (padrão é 'outer')
    ignore_index=False,  	# Ignora os índices existentes e cria novos (padrão é False)
    keys=None,           	# Chaves para associar aos DataFrames/Series resultantes
    levels=None,         	# Níveis específicos para MultiIndex, se fornecido
    names=None,         	# Nomes para os níveis do índice resultante
    verify_integrity=False, # Verifica a integridade da concatenação (padrão é False)
    sort=False,          	# Ordena eixos não concatenados se necessário (padrão é False)
    copy=True            	# Copia os dados, em vez de fazer referência direta (padrão é True)
)
```

### **4.4 Reformatação e pivotamento**
#### 4.4.1 Reformatação
A reformatação, também conhecida como "melting", transforma um DataFrame de um formato "largo" para um formato "longo". Isso é útil quando queremos transformar colunas em valores para facilitar agregações ou comparações.

```python 
pd.melt(
    frame,                # DataFrame que será reformado
    id_vars=None,         # Colunas a manter (não derreter)
    value_vars=None,      # Colunas a derreter (transformar em valores)
    var_name=None,        # Nome da nova coluna de variáveis
    value_name="value",   # Nome da nova coluna de valores
    col_level=None,       # Nível de coluna a derreter se houver MultiIndex
    ignore_index=True     # Ignorar o índice original ou não (padrão é True)
)
```

#### 4.4.2 Pivotamento

O pivotamento faz o oposto do "melt", transformando dados de formato "longo" para "largo". Ele reorganiza os dados para que valores de uma coluna se tornem colunas, com base em outra variável.

```python
df.pivot(
    index=None,           # Coluna(s) para usar como índice
    columns=None,         # Coluna(s) cujos valores se tornarão colunas
    values=None           # Coluna(s) cujos valores serão os valores resultantes
)
```

A função pivot_table permite agregar dados, o que não é possível com pivot simples. Ela oferece mais flexibilidade, permitindo calcular médias, somas e outros métodos de agregação.

```python
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
```