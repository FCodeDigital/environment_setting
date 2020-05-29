# Criado um VirtualHost no Xampp (Windows)

Em ambiente local, podemos utilizar esse mesmo artificio, sendo que a utilização do Virtual Host em ambiente local pode ajudar na organização. Se utilizar modo de re-escrita (rewrite), não precisa mudar o .htaccess que está local para o que está em produção.

Se trabalhar com cookies, pode separar por virtual host, sem ter conflito, etc.

Ao invés de utilizar:

```
http://localhost/nomesite
```

Você pode utilizar:

```
http://local.nomesite.com
```

Você pode criar qualquer nome, domínio ou subdomínio de acordo com seu gosto.

Basicamente, vamos configurar o Windows para quando acessar o domínio e apontar para nossa máquina (localhost) no Apache para uma pasta específica.

Acesse o arquivo:

```
C:\Windows\System32\drivers\etc\hosts
```

Você pode acessar com bloco de notas mesmo. Pode ser que você tenha que executar como Administrador.

Nesse arquivo, você encontrará o ip para sua máquina (127.0.0.1) com nome na frente “localhost”. Quando você digitar  “localhost” no seu navegador, ele está apontando para sua máquina, então o Apache (Servidor Web) vai apontar para sua pasta.

Como estamos usando o XAMPP com a premissa de estar instalado no C://, ele irá apontar para: C:\xampp\htdocs.

O seu arquivo host será como esse abaixo:

```
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#	127.0.0.1       localhost
#	::1             localhost
```

Agora adicione o domínio que você deseja como está no localhost. No exemplo, vou criar chamado “local.projeto.com”, ficando assim:

```
127.0.0.1       local.projeto.com
```

Agora será necessário configurar o Apache. Também poderá ser feito com bloco de notas, ou qualquer editor de código.

Acesse o arquivo:

```
C:\xampp\apache\conf\extra\httpd-vhosts.conf
```

Nesse arquivo serão configurados os Virtual Hosts. Ele já vem com configurações de exemplo, porém comentado.

Vamos usá-lo como base:

```
<VirtualHost *:80>
    ##ServerAdmin webmaster@dummy-host.example.com
    ##DocumentRoot "C:/xampp/htdocs/dummy-host.example.com"
    ##ServerName dummy-host.example.com
    ##ServerAlias www.dummy-host.example.com
    ##ErrorLog "logs/dummy-host.example.com-error.log"
    ##CustomLog "logs/dummy-host.example.com-access.log" common
</VirtualHost>
```

* VirtualHost: Tag definindo as configurações do virtual host.
* ServerAdmin: Endereço de contato.
* DocumentRoot: Caminho completo até a pasta que será acessada.
* ServerName: Nome do host que será acessado.
* ServerAlias: Nomes alternativos para o host.
* ErrorLog:  Nome do arquivo que o servidor registrará os erros encontrados.
* CustomLog: Nome do arquivo para as requisições.

Iremos adicionar a nossa configuração, apontando para onde será configurado o virtual host. No nosso projeto seria:

```
C:\xampp\htdocs\projeto
```

Vamos configurar o virtual host:

```
<VirtualHost *:80>
    ServerAdmin webmaster@local.projeto.com
    DocumentRoot "C:/xampp/htdocs/projeto"
    ServerName local.projeto.com
    ErrorLog "logs/local.projeto.com-error.log"
    CustomLog "logs/local.projeto.com--access.log" common
</VirtualHost>
```

O único que não utilizamos é o ServerAlias, pois não teremos nomes alternativos para o ambiente local.

Se você já estiver iniciado o XAMPP, basta parar (Stop) e iniciar (Start) o Apache, caso contrário, basta só iniciar (Start) o Apache.

Agora basta acessa via URL o endereço que foi configurado.