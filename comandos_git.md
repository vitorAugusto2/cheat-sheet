# Comandos GIT

**Configurações inicial**
$ git config --global user.name "[github nome]"
$ git config --global user.email "[github email]"

**Criar Repositório**
$ git init
$ git init [nome do projeto]
$ git clone [url]

**Mudanças**
$ git status
$ git reflog
$ git diff --staged
$ git add [arquivo]
$ git add .
$ git commit -m "[mensagem versao]"
$ git reset --hard "[número commit ou arquivo]"

**Mudanças em grupo**
$ git branch 
$ git branch [nome da branch/staging]
$ git branch -d [nome da branch/staging]
$ git checkout [nome da branch/staging]
$ git checkou -b [branch origem] [branch atual]
$ git merge [nome da branch/staging] master

**Sincronizar mudanças**
$ git pull
$ git push
$ git push --set --upstream origin [nome da branch/staging]


#### Fluxos
**(1) Single Branch**
$ git init → git add → git status → git commit → git status → git push

**(2) Multiple Branch (Team)**
$ git checkout master → git pull → git branch [nova] → mudanças [(1) Single Branch] → git checkout master → git pull → git merge → git push

#### Git .ignore
$ touch .gitignore | definir no arquivo o caminho do arquivo para não subir no controle de versão


## Lembrar
$ git init
$ git add .
$ git status
$ git commit -m "mensagem do commit"
$ git push
$ git branch
$ git checkout [nome da branch]
$ git checkou -b [branch origem] [branch atual]
$ git merge "branch a receber merge"
$ git pull 