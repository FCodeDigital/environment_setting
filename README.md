#fcodedigital.github.io
Repositório com informações de como configurar o ambiente de desenvolvimento básico da FCode

##Instruções de linha de comando GIT
You can also upload existing files from your computer using the instructions below.


Configuração global do Git
```
git config --global user.name "Nome Completo"
git config --global user.email "email@fcode.com.br"
```

####Criar um novo repositório

```
git clone git@gitlab.com:fcode.digital/testes/iugu.git
cd iugu
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

####Push an existing folder

```
cd existing_folder
git init
git remote add origin git@gitlab.com:fcode.digital/testes/iugu.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

####Push an existing Git repository

```
cd existing_repo
git remote rename origin old-origin
git remote add origin git@gitlab.com:fcode.digital/testes/iugu.git
git push -u origin --all
git push -u origin --tags
```