# Criando e utilizando o `docker-compose`

## Como criar o arquivo

Crie um arquivo chamado `docker-compose.yml` na raiz do projeto, especificando as regras do seu container:

Flags:
```
version: É a versão do docker-compose.
volumes: Mapeia um volume da unidade para um do container
restart_policy: Define se o servidor deverá reiniciar em caso de falha.
```

Exemplo de arquivo:
```
version: '3.3'

services:
  web:
    container_name: Auttom
    build:
      context: .
      dockerfile: Dockerfile
    ports:
    - "8080:80"
    volumes:
    - "/home/auttom/userfiles:/var/www/html/"
    deploy:
      restart_policy:
        condition: on-failure
    environment:
        FCODE_ENVIRONMENT: "production"
        FCODE_VERSION: "1.0"
        FCODE_SITE_NAME: "site_name"
        MYSQL_HOST: "localhost"
        MYSQL_PORT: "root"
        MYSQL_USER: "root"
        MYSQL_PASS: "root"
        MYSQL_DBNAME: "db_name"
        GMAPS_KEY: "maps_key"
        EMAIL_PROTOCOL: "smtp"
        EMAIL_HOST: "smtp.example.com"
        EMAIL_PORT: "25"
        EMAIL_USERNAME: "Username"
        EMAIL_USER: "user@exaple.com"
        EMAIL_ADDRESS: "user@exaple.com"
        EMAIL_PASSWORD: "password"
        LOG_THRESHOLD: "0"
        APPLICATION_ENCRYPTION_KEY: "key"
        ADMIN_ENCRYPTION_KEY: "key"
```

## Rodando o docker

Para rodar o projeto execute:
```
$ docker-compose up -d
```

Utilize o `-d` para rodar em background.

Para restartar utilize:
```
$ docker-compose restart
```

Para parar utilize:
```
$ docker-compose stop
```