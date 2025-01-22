# OS (SISTEMA OPERACIONAL)

## Índice

1. **Tabela de Comandos**
   - [Lista de Comandos e Descrições](#tabela-de-comandos)

2. **Introdução ao módulo `os`**
   - [Descrição do módulo](#1-introdução-ao-módulo-os)

3. **Trabalhando com diretórios**
   - [3.1 Verificando o diretório atual](#31-verificando-o-diretório-atual)
   - [3.2 Alterando o diretório de trabalho](#32-alterando-o-diretório-de-trabalho)
   - [3.3 Listando arquivos em um diretório](#33-listando-arquivos-em-um-diretório)

4. **Manipulação de arquivos e diretórios**
   - [4.1 Criando um novo diretório](#41-criando-um-novo-diretório)
   - [4.2 Criando diretórios recursivos](#42-criando-diretórios-recursivos)
   - [4.3 Removendo arquivos e diretórios](#43-removendo-arquivos-e-diretórios)

5. **Informações sobre arquivos**
   - [5.1 Verificando a existência de arquivos ou diretórios](#51-verificando-a-existência-de-arquivos-ou-diretórios)
   - [5.2 Verificando se é arquivo ou diretório](#52-verificando-se-é-arquivo-ou-diretório)
   - [5.3 Obtendo informações sobre arquivos](#53-obtendo-informações-sobre-arquivos)

6. **Trabalhando com variáveis de ambiente**
   - [6.1 Obtendo o valor de uma variável de ambiente](#61-obtendo-o-valor-de-uma-variável-de-ambiente)
   - [6.2 Definindo uma variável de ambiente](#62-definindo-uma-variável-de-ambiente)

7. **Gerenciamento de processos**
   - [7.1 Executando um comando do sistema](#71-executando-um-comando-do-sistema)
   - [7.2 Obtendo o ID do processo](#72-obtendo-o-id-do-processo)

8. **Funções relacionadas ao caminho dos arquivos**
   - [8.1 Juntando caminhos](#81-juntando-caminhos)
   - [8.2 Dividindo um caminho em diretório e arquivo](#82-dividindo-um-caminho-em-diretório-e-arquivo)
   - [8.3 Obtendo o nome do arquivo sem extensão](#83-obtendo-o-nome-do-arquivo-sem-extensão)

9. **OS com dados**
   - [9.1 Carregamento e processamento de múltiplos arquivos de dados](#91-carregamento-e-processamento-de-múltiplos-arquivos-de-dados)
   - [9.2 Automação de tarefas repetitivas](#92-automação-de-tarefas-repetitivas)
   - [9.3 Verificação de existência de arquivos em pipelines de dados](#93-verificação-de-existência-de-arquivos-em-pipelines-de-dados)
   - [9.4 Criação de diretórios para armazenar resultados](#94-criação-de-diretórios-para-armazenar-resultados)
   - [9.5 Organização e limpeza de diretórios de dados](#95-organização-e-limpeza-de-diretórios-de-dados)
   - [9.6 Gerenciamento de variáveis de ambiente em aplicações de ciência de dados](#96-gerenciamento-de-variáveis-de-ambiente-em-aplicações-de-ciência-de-dados)


## Tabela de Comandos

| Comando | Descrição |
| --- | --- |
| os.getcwd() | Obtém o diretório de trabalho atual |
| os.chdir(path) | Muda o diretório de trabalho para o especificado |
| os.listdir(path) | Lista arquivos e diretórios no caminho especificado |
| os.mkdir(path) | Cria um novo diretório |
| os.makedirs(path) | Cria diretórios de forma recursiva |
| os.remove(path) | Remove o arquivo especificado |
| os.rmdir(path) | Remove o diretório vazio especificado |
| os.removedirs(path) | Remove diretórios de forma recursiva |
| os.path.exists(path) | Verifica se o caminho existe |
| os.path.isfile(path) | Verifica se o caminho é um arquivo |
| os.path.isdir(path) | Verifica se o caminho é um diretório |
| os.path.getsize(path) | Obtém o tamanho de um arquivo |
| os.getenv(key) | Obtém o valor de uma variável de ambiente |
| os.environ[key] = value | Define o valor de uma variável de ambiente |
| os.system(command) | Executa um comando no terminal |
| os.getpid() | Obtém o ID do processo atual |
| os.getppid() | Obtém o ID do processo pai |
| os.path.join(path1, path2) | Junta dois ou mais caminhos de forma segura |
| os.path.split(path) | Separa um caminho em diretório e arquivo |
| os.path.splitext(path) | Separa o nome do arquivo de sua extensão |


### 1. **Introdução ao módulo `os`**


O módulo `os` em Python é uma biblioteca padrão que fornece uma maneira de interagir com o sistema operacional. Ele oferece várias funções que permitem realizar operações de manipulação de arquivos e diretórios, gerenciamento de processos e variáveis de ambiente, entre outros.

Ou seja, facilita a interação entre o Python e o sistema operacional. Ele permite que seu código Python seja independente do sistema, o que significa que o mesmo código pode ser executado em diferentes plataformas (Windows, Linux, MacOS) sem muitas modificações.

Para começar a usar o módulo, basta importá-lo:

```python
import os

```

### 2. **Trabalhando com diretórios**



### 2.1. Verificando o diretório atual

Para descobrir em qual diretório seu código está sendo executado, você pode usar a função `os.getcwd()`:

```python
current_directory = os.getcwd()
print(current_directory)

```

### 2.2. Alterando o diretório de trabalho

Se você precisar mudar o diretório de trabalho, use `os.chdir(path)`:

```python
os.chdir("/caminho/para/diretório")

```

### 2.3. Listando arquivos em um diretório

Você pode listar o conteúdo de um diretório usando `os.listdir(path)`:

```python
files = os.listdir("/caminho/para/diretório")
print(files)

```

### 3. **Manipulação de arquivos e diretórios**



### 3.1. Criando um novo diretório

Para criar um novo diretório, você pode usar `os.mkdir(path)`:

```python
os.mkdir("novo_diretorio")

```

### 3.2. Criando diretórios recursivos

Se precisar criar um diretório dentro de outro que não existe, você pode usar `os.makedirs(path)`:

```python
os.makedirs("dir_pai/dir_filho")

```

### 3.3. Removendo arquivos e diretórios

- Para remover um arquivo: `os.remove(path)`

```python
os.remove("arquivo.txt")

```

- Para remover um diretório vazio: `os.rmdir(path)`

```python
os.rmdir("diretorio_vazio")

```

- Para remover diretórios e seus conteúdos recursivamente: `os.removedirs(path)`

```python
os.removedirs("dir_pai/dir_filho")

```

### 4. **Informações sobre arquivos**



### 4.1. Verificando a existência de arquivos ou diretórios

Você pode verificar se um arquivo ou diretório existe usando `os.path.exists(path)`:

```python
if os.path.exists("arquivo.txt"):
    print("O arquivo existe.")

```

### 4.2. Verificando se é arquivo ou diretório

Para saber se o caminho é um arquivo ou um diretório:

- Arquivo: `os.path.isfile(path)`
- Diretório: `os.path.isdir(path)`

```python
if os.path.isfile("arquivo.txt"):
    print("É um arquivo.")

```

### 4.3. Obtendo informações sobre arquivos

Você pode obter o tamanho de um arquivo usando `os.path.getsize(path)`:

```python
size = os.path.getsize("arquivo.txt")
print(f"Tamanho: {size} bytes")

```

### 5. **Trabalhando com variáveis de ambiente**



As variáveis de ambiente são úteis para armazenar informações específicas do sistema, como o caminho do Python ou outras configurações do sistema operacional.

### 5.1. Obtendo o valor de uma variável de ambiente

Você pode usar `os.getenv(key)` para pegar o valor de uma variável de ambiente:

```python
home_dir = os.getenv("HOME")
print(f"Diretório home: {home_dir}")

```

### 5.2. Definindo uma variável de ambiente

Para definir uma variável de ambiente, use `os.environ[key] = value`:

```python
os.environ["MEU_VAR"] = "valor"

```

### 6. **Gerenciamento de processos**



O módulo `os` também permite iniciar novos processos e interagir com processos do sistema.

### 6.1. Executando um comando do sistema

Você pode usar `os.system()` para executar comandos diretamente no terminal ou prompt de comando:

```python
os.system("ls")  # Comando Linux para listar arquivos
os.system("dir")  # Comando Windows para listar arquivos

```

### 6.2. Obtendo o ID do processo

Para obter o ID do processo atual ou do processo pai:

- ID do processo atual: `os.getpid()`
- ID do processo pai: `os.getppid()`

```python
pid = os.getpid()
print(f"O ID do processo atual é: {pid}")

```

### 7. **Funções relacionadas ao caminho dos arquivos**



O módulo `os` também inclui subfunções para manipulação de caminhos de arquivos e diretórios. Elas estão disponíveis através de `os.path`.

### 7.1. Juntando caminhos

Para criar um caminho de arquivo ou diretório de maneira segura para diferentes sistemas operacionais:

```python
path = os.path.join("/home", "usuario", "documento.txt")
print(path)  # Saída no Linux: /home/usuario/documento.txt

```

### 7.2. Dividindo um caminho em diretório e arquivo

Para separar o caminho de um diretório do nome de um arquivo, use `os.path.split(path)`:

```python
dir_name, file_name = os.path.split("/home/usuario/documento.txt")
print(dir_name)  # Saída: /home/usuario
print(file_name)  # Saída: documento.txt

```

### 7.3. Obtendo o nome do arquivo sem extensão

Para obter o nome do arquivo sem sua extensão, use `os.path.splitext(path)`:

```python
file_name, file_ext = os.path.splitext("documento.txt")
print(file_name)  # Saída: documento
print(file_ext)   # Saída: .txt

```

# OS com dados



Na área de ciência de dados, o módulo `os` é frequentemente utilizado para tarefas relacionadas à manipulação de arquivos e diretórios, especialmente em situações que envolvem automação de processos, organização de arquivos de dados e gerenciamento de pipelines. Vou apresentar alguns exemplos práticos e comuns onde o módulo `os` é amplamente utilizado.

### 1. **Carregamento e processamento de múltiplos arquivos de dados**

Cientistas de dados frequentemente precisam carregar vários arquivos (como arquivos CSV, Excel, JSON, etc.) para realizar análises. O módulo `os` pode ajudar a navegar por diretórios, identificar e carregar os arquivos necessários.

### Exemplo: Carregar todos os arquivos CSV de um diretório

```python
import os
import pandas as pd

# Caminho do diretório com os arquivos CSV
data_dir = "caminho/para/diretorio"

# Lista para armazenar os dataframes
dataframes = []

# Percorrer todos os arquivos no diretório
for filename in os.listdir(data_dir):
    if filename.endswith(".csv"):  # Verifica se o arquivo tem extensão .csv
        file_path = os.path.join(data_dir, filename)  # Cria o caminho completo do arquivo
        df = pd.read_csv(file_path)  # Carrega o CSV em um dataframe
        dataframes.append(df)  # Adiciona o dataframe à lista

# Concatenar todos os dataframes em um único dataframe
final_df = pd.concat(dataframes, ignore_index=True)

print(final_df.head())

```

Neste exemplo, usamos o `os.listdir()` para listar os arquivos no diretório e o `os.path.join()` para garantir que os caminhos sejam formados corretamente. Isso é útil quando você está trabalhando com grandes volumes de dados divididos em múltiplos arquivos.

### 2. **Automação de tarefas repetitivas**

Imagine que você tenha que analisar dados que são atualizados periodicamente e armazenados em diferentes subdiretórios. Você pode automatizar o processo de busca de arquivos e geração de relatórios usando `os`.

### Exemplo: Renomear múltiplos arquivos de dados automaticamente

Às vezes, você pode precisar renomear arquivos para um formato padronizado.

```python
import os

# Diretório com os arquivos que precisam ser renomeados
data_dir = "caminho/para/diretorio"

# Renomear os arquivos CSV para um formato padrão
for filename in os.listdir(data_dir):
    if filename.endswith(".csv"):
        old_file_path = os.path.join(data_dir, filename)
        # Criar um novo nome de arquivo com um prefixo
        new_file_path = os.path.join(data_dir, f"processed_{filename}")
        os.rename(old_file_path, new_file_path)

print("Arquivos renomeados com sucesso.")

```

Isso é útil quando você recebe arquivos de diferentes fontes e precisa padronizar seus nomes para processá-los de forma mais organizada.

### 3. **Verificação de existência de arquivos em pipelines de dados**

Em pipelines de dados, muitas vezes você precisa garantir que certos arquivos existem antes de processá-los, evitando erros futuros no código.

### Exemplo: Verificar se um arquivo de dados existe antes de carregar

```python
import os
import pandas as pd

file_path = "caminho/para/diretorio/dados.csv"

# Verificar se o arquivo existe antes de tentar carregá-lo
if os.path.exists(file_path):
    df = pd.read_csv(file_path)
    print("Arquivo carregado com sucesso!")
else:
    print(f"O arquivo {file_path} não foi encontrado.")

```

Este exemplo é uma boa prática para evitar erros em tempo de execução, como `FileNotFoundError`, que podem ocorrer quando se tenta abrir um arquivo que não existe.

### 4. **Criação de diretórios para armazenar resultados**

Durante a análise de dados, você frequentemente gera saídas, como gráficos, relatórios ou arquivos processados. O módulo `os` pode ser usado para criar diretórios de forma programática para salvar esses resultados.

### Exemplo: Criar diretório para salvar gráficos gerados

```python
import os
import matplotlib.pyplot as plt

# Diretório para salvar os gráficos
output_dir = "caminho/para/salvar/graficos"

# Verifica se o diretório já existe, caso contrário, cria-o
if not os.path.exists(output_dir):
    os.makedirs(output_dir)

# Gerar e salvar um gráfico simples
plt.plot([1, 2, 3], [4, 5, 6])
plt.title("Exemplo de Gráfico")
output_file = os.path.join(output_dir, "grafico_exemplo.png")
plt.savefig(output_file)

print(f"Gráfico salvo em: {output_file}")

```

Neste exemplo, `os.makedirs()` garante que o diretório seja criado caso ainda não exista, facilitando a organização dos arquivos gerados automaticamente durante a execução de scripts de análise de dados.

### 5. **Organização e limpeza de diretórios de dados**

Na ciência de dados, você pode gerar grandes quantidades de arquivos temporários, como versões intermediárias de dados processados. O módulo `os` pode ser utilizado para automatizar a exclusão desses arquivos.

### Exemplo: Remover arquivos temporários de um diretório

```python
import os

# Diretório com os arquivos temporários
temp_dir = "caminho/para/temp/diretório"

# Excluir todos os arquivos com extensão .tmp
for filename in os.listdir(temp_dir):
    if filename.endswith(".tmp"):
        file_path = os.path.join(temp_dir, filename)
        os.remove(file_path)

print("Arquivos temporários removidos.")

```

Esse tipo de automação é útil para manter os diretórios limpos e evitar o acúmulo de arquivos desnecessários, o que pode melhorar a organização e a eficiência.

### 6. **Gerenciamento de variáveis de ambiente em aplicações de ciência de dados**

Quando você trabalha com bibliotecas como TensorFlow ou PyTorch, ou quando configura pipelines de dados, pode ser necessário definir variáveis de ambiente específicas, como caminhos para bibliotecas, chaves de API ou credenciais de banco de dados.

### Exemplo: Definir variáveis de ambiente para um pipeline de dados

```python
import os

# Definir a variável de ambiente com a chave da API
os.environ["API_KEY"] = "minha_chave_secreta"

# Acessar a variável de ambiente posteriormente no código
api_key = os.getenv("API_KEY")

# Usar a chave da API para fazer requisições a um serviço de dados, por exemplo
print(f"Chave da API: {api_key}")

```

Esse tipo de abordagem é útil para tornar o código mais seguro, evitando a inserção direta de informações sensíveis no script.
