# PYTHON

## Índice

- [1. Saída de dados com f-string](#1-saída-de-dados-com-f-string)
- [2. Variáveis e Entrada de dados](#2-variáveis-e-entrada-de-dados)
- [3. Estrutura Condicional](#3-estrutura-condicional)
- [4. Estrutura de repetição](#4-estrutura-de-repetição)
- [5. Lista, dicionários, tuplas e conjuntos](#5-lista-dicionários-tuplas-e-conjuntos)
    - [**5.1 Lista**](#51-lista)
    - [**5.2 Dicionários**](#52-dicionários)
    - [**5.3 Tuplas**](#53-tuplas)
    - [**5.4 Conjuntos**](#54-conjuntos)
- [6. String](#6-string)
- [7. Funções](#7-funções)
    - [**7.1 Exceções**](#71-exceções)
    - [**7.2 Módulos**](#72-módulos)
- [8. Arquivo](#8-arquivo)
- [9. Classes e Objetos](#9-classes-e-objetos)
    - [**9.1 Objeto**](#91-objeto)
    - [**9.2 Passagem de paramêtro**](#92-passagem-de-paramêtro)
    - [**9.3 Herança**](#93-herança)
- [10. Formatação de espaco em branco](#10-formatação-de-espaco-em-branco)
- [11. Defaultdict e Counter](#11-defaultdict-e-counter)
- [12. Teste Automatizados e Asserção](#12-teste-automatizados-e-asserção)
- [13. Iteráveis e Geradores](#13-iteráveis-e-geradores)
- [14. Zips e Descompactação de Argumento](#14-zips-e-descompactação-de-argumento)
- [15. Anotações de Tipo (Tipagem)](#15-anotações-de-tipo-tipagem)

## 1. Saída de dados com f-string
---

```python
# print
a = "mundo"
print(f"Olá {a}")
```

```python
preço = 5.20
print(f"preço: {preço:10.2f}")
print(f"preço: {preço:>10.2f}")
print(f"preço: {preço:<10.2f}")
print(f"preço: {preço:^10.2f}")
print(f"preço: {preço:.^10.2f}")
print(f"preço: {preço:x^10.2f}")
print(f"preço: {preço:_^10.2f}")
print(f"preço: {preço * 10 + 1 :5.2f}")
```

```python
# f-string
x = 5.1
print(f"inteiro: {int(x)}")
```

```python
# Multilinhas
print(f"""
    O preço do novo produto é: {preço:5.2f}
    calculos: {preço * 10 + 1 :5.2f}
    inteiro: {int(x)}
    """)
```

## 2. Variáveis e Entrada de dados
---

```python
# Operadores relacionais
a = 1
b = 5
c = 2
d = 1

a == b 
a > d
a < d
c != c
a >= b
d <= a

# Operadores Lógicos
True and True
False or True
not True
```

```python
# Expressões lógicas
True or False and not True

# Veracidade
x = None 
False
None
[]
{}
""
set()
0
0.0

## and
safe_x = x or 0
safe_x = x if x is not None else 0

## all e any
all([True, 1, {3}])
all([True, 1, {}])
any([True, 1, {}])
any([])
```

```python
# Entrada de dados e conversão 
anos = int(input("Anos de serviço: "))
valor_por_anos = float(input(f"Valor por ano: "))
bonus = anos * valor_por_anos
print(f"Bonus: {bonus: 5.2f}")
```

## 3. Estrutura Condicional
---

```python
# if e else
idade = int(input("Digite a idade de seu carro: "))

if idade <= 3:
    print(f"Seu carro é novo !")
else:
    print(f"Seu carro é velho !")
```

```python
# elif
categoria = int(input("Digite a categoria do produto: "))

if categoria == 1:
    preco = 10
elif categoria == 2:
    preco = 20
elif categoria == 3:
    preco = 30
else:
    print(f"Categoria invalida, digite um valor entre 1 e 3 !")
    
print(f"Preco do produto {preco: 6.2f}")
```

```python
# Ternário
par_ou_impar = "par" if x % 2 == 0 else "impar"

x = 2
print(par_ou_impar)
```

## 4. Estrutura de repetição
---

```python
# while
ultimo = int(input("Digite o ultimo digito de contagem: "))
i = 0
while i <= ultimo:
    if i % 2 == 0:
        print(i)
    i += 1 

##
   
n = 1
soma = 0
while n <= 10:
    x = int(input(f"Digite o {x} numero:"))
    soma += x 
    n += 1 
print(f"Soma = {soma}")
```

```python
# Break
s = 0
while True:
    v = int(input("Digite um numero a somar ou 0 para sair:"))
    if v == 0:
        break 
    s += v 
print(s)
```

```python
# Continue
i = 0 
while i < 12:
    i += 2
    if i == 8:
        continue 
    print(i)
else:
    print(f"Os numeros pares de 2 a 12 foram exibidos, com excecao do 8")
```

```python
# While aninhados
tabuada = 1
while tabuada <= 10:
    numero = 1
    while numero <= 10:
        print(f"{tabuada} x {numero} = {tabuada * numero}")
        numero += 1
    tabuada += 1
```

## 5. Lista, dicionários, tuplas e conjuntos
---

### **5.1 Lista**

```python
# Tipos
integer_list = [1, 2, 3]
heterogeneous_list = ["string", 0.1, True]
list_of_list = [integer_list, heterogeneous_list, []]
```

```python
l1 = []
l2 = [0, 1, 2, 3, 4, 5]

# Fatiamento
print(l2[2])
print(l2[0:5])
print(l2[:4])
print(l2[1:3])
print(l2[-1])
print(l2[1:-1])

# Cópia
print(l2[:])    

# stride
print(l2[::2])
print(l2[5:2:-1])

# Tamanho 
len(l2)

# Adicao 
## append
l2.append("x")
print(l2)

l2 = l2 + [1]
l2 = l2 + [6, 7, 8]
print(l2)

## extend
l2.extend("y")
l2.extend([20, 30, 40])
print(l2)

## insert
l2.insert(3, "z") 
print(l2)

# Removendo
## del
del l2[0]
print(l2)

## pop
l2.pop(2)
print(l2)

## remove
l2.remove(1)
print(l2)

# Verificaicao
1 in l2     # True
20 in l2    # False
```

```python
# Pesquisa 
z = ["a", "b", "c", "d"]
letra = str(input("Digite a letra: "))

## while (sequencial)
while x < len(z):
    if z[x] == letra:
        print("achou")
        break
    x += 1
else:
    print("nao achou")

## for (um a um)
for x in z:
    if x == letra:
        print("achou")
        break
    else:
        print("nao achou")

## range
for i in range(len(z)):
    if z[i] == letra:
        print("achou")
        break
    else:
        print("nao achou")
```

```python
# Lista Aninhadas
la = [4, [2, 3], [1, [3, 4]]]

print(la[2][1])
print(la[2][1][0])

## matriz
a = [[1,2,3],
     [4,5,6],
     [7,8,9]]

print(a)
print(a[0])
print(a[0][1])
a[1][2] = 50
print(a)

for i in range(len(a)):            
     for j in range(len(a[i])):    
        print(a[i][j], end=" ")    
     print()                       

```

```python
# classificacao
x = [4, 1 , 2, 3]
y = sorted(x)       
x.sort()            

##

x = sorted([-4, 1, -2, 3], keys=abs, reverse=True)  

##

wc = sorted(word_counts.items(),
            key= lambda word_and_count: word_and_count[1],
            reverse=True)
```

```python
# Compreensoes de listas
l1 = [x for x in range(5) if x % 2 == 0]    # [0, 2, 4]
l2 = [x * x for x in range(5)]              # [0, 1, 4, 9, 16]
l3 = [x * x for x in l1 ]                   # [0, 4, 16]

## transformar lista em dicionarios ou conjuntos
l_dict = {x: x * x for x in range(5)}  
l_set = {x * x for x in [1, -1]}       

## sem valor da lista
zeros = [0 for _ in l1]

## multiplos fors
pairs =[(x, y)
        for x in range(10)
        for y in range(x + 1, 10)]
```

### **5.2 Dicionários**

```python
# Tipos
empty_dict = {}
estoque = {
    "tomate" : [1000, 2.30],
    "alface" : [500, 0,45],
    "batata" : [2001, 1.20]
}
dict = { 
    "nome" : "Fulano",
    5 : "cinco",
    "lista" : [1, 2, 4]
}

```

```python
# Pesquisa
dict["nome"]

# Atribuiçao
dict[5] = "four" 

# Remoção
del dict["lista"]   

# Verificação
print(5 in dict)  
  
## keys
print(dict.keys()) 

## values     
print(dict.values())    

## items
print(dict.items())     

# Retornando todas as chaves em tupla
for chave, valor in dict.items():
    print(chave)

# get
l2.get("nome", 0)
```

### **5.3 Tuplas**

```python
# Tipo
tupla = "a", "b", "c"
tupla = ("a", "b", "c") 

print(tupla)
print(tupla[1])
```

```python
# Retornar multiplos valores
def sum_and_product(x, y):
    return (x + y), (x * y)

sp = sum_and_product(2, 3)      
s, p = sum_and_product(5, 10)   
```

```python
# Atribuições simples
x, y = 1, 2     
x, y = y, 2     
```

### **5.4 Conjuntos**

```python
# set
a = set()
a.add(1)
a.add(2)
a.add(3)
print(a)
a.add(1)
print(a)
a.add(0)
a.add(-1)
print(a)

##

b = set([2, 3])
print(b)
len(b)
2 in b
```

```python
item_list = [1, 2, 3, 1, 2, 3]
num_items = len(item_list)         
item_set = set(item_list)           
num_disctinct_items = len(item_set) 
distinct_item_list = list(item_set)
```

## 6. String
---

```python
# Strings literais
a = 'one way of writing a string'
b = "another way"

# Multilinhas
c = """
This is a longer string that
spans multiple lens
"""
```

```python
# Tratar como sequencia de lista ou tuplas
l = list("Alo mundo")
l[0] = "a"
print(l)

# Junta os caracteres
s = "".join(l)
print(s)
```

```python
s = "O rato roeu a roupa do Rei de Roma"

# lower
s.lower()

# upper
s.upper()

# in ou not in 
"rato" in s.lower()

```

```python
t = "Um tigre, dois trigres, tres tigres"

# Contagem
t.count("tigre")
t.count("t")

# Pesquisa
t.find("tig")
t.rfind("e")

# split
s.split(" ")

# replace
s.replace("tigre", "gato")

# remocao de espaco branco
t.strip()
t.rstrip()
t.lstrip()
```

```python
s = "125"
p = "alo mundo"

# Validacao
p.isalnum()
s.isaplha()
p.isupper()
p.islower()

# Formatacao f-string
f_string = f"s= {s}, p={p}"
```

```python
# Concatenação
nome = "Vitor"
sobrenome = "Lemes"

nome + "Augsuto"
nome + "Augusto" + sobrenome
```

## 7. Funções
---

```python
# def
def soma(a, b):
    print(a + b)
soma(2, 5)

# return
def soma(a, b):
    return a + b
print(soma(2, 5))
```

```python
# if e else
def épar(x):
    return x % 2 == 0

def par_ou_impar(x):
    if épar(x):
        return "par"
    else:
        return "impar"

print(par_ou_impar(4))
print(par_ou_impar(5))
```

```python
# Recursividade
def fatorial(n):
    if n == 0 or n == 1:
        return 1
    else:
        return n * fatorial(n-1)

##

def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)
```

```python
# lambda
aumento = lambda a, b: (a*b/100)
aumento(100, 50)

##

def apply_to_one(f):
    return f(1)

y = apply_to_one(lambda x: x + 4)
```

```python
# Parametros recebendo argumentos
def my_print(message = "my default message"):
    print(message)

my_print("hello")  
my_print()         
```

### **7.1 Exceções**

```python
# try e except
nomes = ["Ana", "Carlos", "Maria"]
for tentativa in range(3):
    try:
        i = int(input("Digite o indice que quer imprimir: "))
        print(nomes[i])
    except Exception as e:
        print(f"Algo deu errado: {e}")
```

### **7.2 Módulos**

```python
# entrada.py
def valida_inteiro(mensagem, minimo, maximo):
    while True:
        try:
            v = int(input(mensagem))
            if v >= minimo and v <= maximo:
                return v
            else:
                print(f"Digite um valor entre {minimo} e {maximo}")
        except ValueError:
            print("Voce deve digitar um numero inteiro")

# soma.py
import entrada
l = []
for x in range(10):
    l.append(entrada.valida_inteiro("Digite um numero:", 0 , 20))
print(f"Soma: {sum(l)}")
```

```python
"""
import matplotlib                               -> importar
import matplotlib as plt                        -> alias
from collections import defaultdict, Counter    -> valores especificos
from re import *                                -> importar conteudo inteiro
"""
```

## 8. Arquivo
---

```python
# r, w, a, +
with open("test.txt", "w") as multiplos4:
    with open("pares.txt") as pares:
        for l in pares.readlines():
            if int(l) % 4 == 0:
                multiplos4.write(l)

# OS
import os
os.getcwd()
os.mkdir("x")
os.makedirs("y/z")
os.rename("x", "x2")
os.remove("test.txt")
os.listdir("x2")

## isdir e isfile
import os.path

for a in os.listdir("."):
    if os.path.isdir(a):
        print(f"{a}/")
    elif os.path.isfile(a):
        print(a)

## Verificação
if os.path.exists("z"):
    print("O diretorio z existe")
else:
    print("O diretorio z nao existe")
```

## 9. Classes e Objetos 
---

### **9.1 Objeto**

```python
# classe - associa dados e operacoes em uma só estrutura
# objeto - instancia/variavel de uma classe
#
# __init__ -> construtor
# - definir o compratmento de todos os objetos de uma classe (metodos), preservando os valores individuas de cada um (atributos)
class Televisao: # padrao PascalCase
    def __init__(self):         # construtor/inicializador
        self.ligada = False     # atributo; self = refere a instancia da classe especifica
        self.canal = 2      
    
    def muda_canal_para_baixo(self):    # metodo é associado a uma classe e atua sobre um objeto
        self.canal -= 1                 # modifica atributo

    def muda_canal_para_cima(self):    
        self.canal += 1                
```

```python
## caso 1
tv = Televisao()    # instancia objeto
tv.ligada           # False
tv.canal            # 2

tv_sala = Televisao()   # instancia objeto
tv_sala.ligada = True   # modifica valor do atributo
tv_sala.canal = 4       # modifica valor do atributo
tv.canal                # 2
tv_sala.canal           # 4

## caso 2
tv = Televisao()
tv.muda_canal_para_cima()
tv.muda_canal_para_cima()
tv.canal    # 4

tv.muda_canal_para_baixo()
tv.canal    # 3
```

### **9.2 Passagem de paramêtro**

```python
class Televisao:
    # passa parametro
    def __init__(self, min, max) -> None: 
        self.ligada = False
        self.canal = 2
        self.cmim = min
        self.cmax = max

    def muda_canal_para_baixo(self):
        if self.canal - 1 >= self.cmim:
            self.canal -= 1

    def muda_canal_para_cima(self):
        if self.canal + 1 <= self.cmax:
            self.canal += 1

tv = Televisao(1, 99)

for x in range(0, 120):
    tv.muda_canal_para_cima()
print(tv.canal) 

for x in range(0, 120):
    tv.muda_canal_para_baixo()
print(tv.canal) 
```

```python
class CountingClicker:
    def __init__(self, count = 0):
        self.count = count

    def __repr__(self):
        return f"CountingClicker(count={self.count})"
    
    def click(self, num_times = 1):
        self.count += num_times
    
    def read(self):
        return self.count

    def reset(self):
        self.count = 0

clicker = CountingClicker()
assert clicker.read() == 0, "clicker should start with count 0"
clicker.click()
clicker.click()
assert clicker.read() == 2, "after two clicks, clicker should have count 2"
clicker.reset()
assert clicker.read() == 0, "afeter reset, clicker should be back to 0"
```

#### **9.3 Herança**

```python
class Conta:
    pass

class ContaEspecial(Conta): # ContaEspecial herda de Conta
    def __init__(self, clientes, numero, saldo=0, limite=0) -> None:
        Conta.__init__(self, clientes, numero , saldo)
        self.limite = limite
    def saque(self, valor):
        if self.saldo + self.limite >= valor:
            self.saldo -= valor
            self.operecaoes.append(["SAQUE", valor])
    
```

## 10. Formatação de espaco em branco
---

```python
# Sem tabulação
long_winded_computation = (1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 +
                           9 + 10 + 11)

# Com tabulação
two_plus_three = 2 + \
                 3
```

## 11. Defaultdict e Counter
---

```python
from collections import defaultdict, Counter

# defaultdict
dd_list = defaultdict(list)
dd_list[2].append(1)

# counter
c = Counter([0, 1, 2, 0]) 
```

## 12. Teste Automatizados e Asserção
---

```python
def smalltest_item(xs):
    return min(xs)

# verifica se o codigo esta correto 
assert smalltest_item([10, 20, 5, 40]) == 5     # Ok
assert smalltest_item([1, 0 , -1, 2]) == 0      # msg: AssertionError
```

## 13. Iteráveis e Geradores
---

```python
# gerador 
def generate_range(n):
    i = 0
    while i < n:
        yield i     # cada chamada para yield produz um valor do gerador
        i += 1
        
evens_below_20 = (i for i in generate_range(20) if i % 2 == 0)
```

```python
# enumerate
for i, name in enumerate(names):
    print(f"idx_name = {i} : value_name {name}")
```

## 14. Zips e Descompactação de Argumento
---

```python
# zip
l1 = ['a', 'b', 'c']
l2 = [1, 2, 3]
[pair for pair in zip(l1, l2)] # [('a', 1), ('b', 2), ('c', 3)]
```

```python
# descompactacao do argumento
pairs = [('a', 1), ('b', 2), ('c', 3)]
lettres, numbers = zip(*pairs)

##

lettres, numbers = zip(('a', 1), ('b', 2), ('c', 3))
```

## 15. Anotações de Tipo (Tipagem)
---

```python
# tipada dinamicamente
def add(a, b):
    return a + b

# tipada eestaticamente
def add(a: int, b: int) -> int:
    return a + b

# Vector

def dot_product(x, y): ...
def dot_product(x: Vector, y: Vector) -> float: ...

# Union

def secretly_ugly_function(value, operation): ...
def secretly_ugly_function(value: int,
                           operation: Union[str, int, float, bool]) -> int: ...
```

```python
# typing
## List
from typing import List 
def total(xs: List[float]) -> float:
    return sum(total)

## Optional

from typing import Optional
values: List[int] = []          
best_so_far = Optional[float]   
```
