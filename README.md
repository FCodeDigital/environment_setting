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

#Criando chaves SSH

Esta documentação é um resumo traduzido da documentação do Gitlab. Para ler a original acesse a [Wiki](https://gitlab.com/help/ssh/README#generating-a-new-ssh-key-pair).

## Requisitos

O único requisito é ter o cliente OpenSSH instalado em seu sistema.Isso vem pré-instalado no GNU / Linux e no macOS, mas não no Windows.

Dependendo da sua versão do Windows, existem diferentes métodos para trabalhar com chaves SSH.

### Instalando o cliente SSH para o Windows 10

A partir do Windows 10, você pode[instalar o Windows Subsystem para Linux (WSL), no](https://docs.microsoft.com/en-us/windows/wsl/install-win10)qual é possível executar distribuições do Linux diretamente no Windows, sem a sobrecarga de uma máquina virtual.Uma vez instalado e configurado, você terá os clientes Git e SSH à sua disposição.

### Instalando o cliente SSH para o Windows 8.1 e o Windows 7

A maneira mais fácil de instalar o Git e o cliente SSH no Windows é o[Git for Windows](https://gitforwindows.org).Ele fornece uma emulação BASH (Git Bash) usada para executar o Git a partir da linha de comando e o`ssh-keygen`comando que é útil para criar chaves SSH como você aprenderá abaixo.

### Gerando um novo par de chaves SSH

1.  Abra o terminal do Linux/Mac OS ou o Git Bash no Windows
2.  Gere uma nova chave SSH ED25519
`ssh-keygen -t ed25519 -C "email@example.com"`
Ou gere uma chave RSA, se a primeira não funcionar:
`ssh-keygen -o -t rsa -b 4096 -C "email@example.com"`
3.  A seguir você será solicitado a definir um caminho para salvar a nova chave. Pressione Enter para manter o padrão.
4.  Após definir um caminho você será solicitado a definir uma senha para proteger seu novo par de chaves. É recomendado que seja definida uma senha, mas ela não é obrigatória. Você pode pular a criação de senha pressionando Enter duas vezes.

### Adicionando uma chave SSH à sua conta do GitLab

1.  Copie sua chave SSH **pública** para a área de transferência usando um dos comandos abaixo, dependendo do seu sistema operacional:

**MacOS:**

```shell
$ pbcopy < ~/.ssh/id_ed25519.pub
```
**Linux (requer o pacote xclip):**

```shell
$ xclip -sel clip < ~/.ssh/id_ed25519.pub
```
**Git Bash no Windows:**

```shell
$ cat ~/.ssh/id_ed25519.pub | clip
```
Você também pode abrir a chave em um editor de texto e copiá-la de lá, mas tenha cuidado para não alterar nada acidentalmente.

NOTA: **Nota:** Se você optou por criar uma chave RSA, o nome poderá ser diferente.

2.  Adicione sua chave SSH pública à sua conta do GitLab clicando no seu avatar no canto superior direito e selecionando **Configurações**.A partir daí, navegue para as **Chaves SSH** e cole sua chave pública na seção "Chave". Se você criou a chave com um comentário, isso aparecerá em "Título".Se não, dê a sua chave um título identificável como_Work Laptop_ou_Home Workstation_e clique em **Add key**.

NOTA: **Nota:** Se você copiou manualmente sua chave SSH pública, copie a chave inteira, começando com`ssh-ed25519`(ou`ssh-rsa`) e terminando com o seu e-mail.

## Testando que tudo está configurado corretamente

Para testar se sua chave SSH foi adicionada corretamente, execute o seguinte comando no seu terminal (substituindo`gitlab.com`pelo domínio de instância do seu GitLab):

```shell
$ ssh -T git@gitlab.com
```
Você deve receber uma_Welcome to GitLab`@username`!_mensagem.

Se a mensagem de boas vindas não aparecer, execute o modo detalhado do SSH substituindo`-T`por`-vvvT`para entender onde está o erro.

### Salvando a senha da chave no Windows

```shell
$ eval `ssh-agent -s`
$ ssh-add ~/.ssh/*_rsa
```