# Install Nginx on Ubuntu

## Update system and install
```
$ sudo apt update
$ sudo apt install nginx
```

## Adjusting the Firewall

```
$ sudo ufw app list
$ sudo ufw allow 'Nginx HTTP'
$ sudo ufw allow 'Nginx HTTPS'
$ sudo ufw status
```

## Verificando o servidor

```
$ systemctl status nginx
```

## Mexendo no Nginx

Parando o servidor:
```
$ systemctl stop nginx
```

Iniciando o servidor:
```
$ systemctl start nginx
```

Reiniciando o servidor:
```
$ systemctl restart nginx
```

Para mudar as configurações sem reiniciar o servidor:
```
$ systemctl reload nginx
```

Para re-ativar o serviço do servidor:
```
$ systemctl enable nginx
```

## Configurando o servidor

Apague os arquivos em `sites-enables` e `sites-available`.

```
$ cd /etc/nginx
$ cd /sites-enabled && rm default
$ cd /etc/nginx
$ cd /sites-available && rm default
```
Apague o arquivo de configuração `default`

```
$ cd /etc/nginx
$ cd /conf.d && rm default
```

Crie um arquivo de configuração para cada domínio que deseja ter dentro da pasta `conf.d`.

```
$ cd /etc/nginx/conf.d
$ touch sub-domain-com-br.conf
$ nano sub-domain-com-br.conf
```

Coloque o conteúdo abaixo no arquivo .conf

```
server {
    listen 80; //SUBSTITUIR COM A PORTA QUE SERÁ ACESSADA, O PADRÃO É 80
    server_name sub.domain.com.br;

   location / {
       proxy_set_header Host $host;
       proxy_set_header X-Forwarded-Proto $scheme;
       proxy_set_header X-Forwarded-Port $server_port;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       proxy_set_header Upgrade $http_upgrade;
       proxy_set_header Connection "upgrade";
       proxy_pass http://127.0.0.1:8080; //SUBSTITUIR COM A PORTA QUE O CONTAINER IRÁ RODAR
       proxy_http_version 1.1;

       proxy_buffer_size 128k;
       proxy_buffers 4 256k;
       proxy_busy_buffers_size 256k;

       # This allows the ability for the execute shell window to remain open for up to 15 minutes. Without this parameter, the default is 1 minute and will automatically close.
       proxy_read_timeout 900s;
    }
}
```

Para colocar o header no nginx ao invés do código, utilize o código abaixo:

```
location / {
    # 1. hide the Access-Control-Allow-Origin from the server response
    proxy_hide_header Access-Control-Allow-Origin;
    # 2. add a new custom header that allows all * origins instead
    add_header Access-Control-Allow-Origin *;
}
```

Rode um reload:

```
$ systemctl restart nginx
$ systemctl reload nginx
```

## Instalando o Let's Encrypt

Em versões ubuntu mais antigas, utilize
```
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt install python-certbot-nginx
```

Nas novas versões a instalação pode ser feita utilizando:
```
$ sudo apt-get install python3-certbot-nginx
```

## Configurando o SSL nos domínios

```
$ sudo certbot --nginx -d sub.domain.com.br -d sub2.domain.com.br
```

Você verá o seguinte retorno:

```
Output
Please choose whether or not to redirect HTTP traffic to HTTPS, removing HTTP access.
-------------------------------------------------------------------------------
1: No redirect - Make no further changes to the webserver configuration.
2: Redirect - Make all requests redirect to secure HTTPS access. Choose this for
new sites, or if you're confident your site works on HTTPS. You can undo this
change by editing your web server's configuration.
-------------------------------------------------------------------------------
Select the appropriate number [1-2] then [enter] (press 'c' to cancel):
```

Escolha a opção 2.

## Verificando a auto renovação do certificado

```
$ sudo certbot renew --dry-run
```

## Instalando o docker

Pule essa etapa se já estiver com o docker configurado

```
$ sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ docker-compose --version
$ apt install docker.io
```

## Mexendo no docker

Você pode ver as imagens com:
```
$ docker images
```

Você pode ver os containers com:
```
$ docker ps
```

Você pode parar um container com:
```
$ docker stop <container_id_or_name>
```

Você pode remover um container com:
```
$ docker rm <container_id_or_name>
```

Você pode acessar um container usando:
```
docker container exec -it <container_id_or_name> bash
```

## Buildando um Dockerfile

```
$ docker build --tag <name_of_build>:1.0 .
```

## Rodando um container

Crie um arquivo de variáveis:
```
$ touch env.list
$ nano env.list
```

Insira as variáveis necessárias para o projeto, como, por exemplo:
```
ENVIRONMENT=production
MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_USER=root
MYSQL_PASS=root
MYSQL_DBNAME=nome_banco
```

Inicie o container:
```
$ docker run --publish 8080:80 --env-file env.list --detach --name <name_of_container> <name_of_build>:1.0 | grep VAR
```

Em `--publish`, o primeiro parâmetro indica a porta que o container rodará dentro do servidor.
