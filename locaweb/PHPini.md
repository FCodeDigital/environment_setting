
## Alterando configurações do PHP

Use essas instruções para alterar as configurações do PHP nos servidores Locaweb.

Crie um arquivo `php.ini` na raiz do projeto e insira o conteúdo abaixo. Modificando conforme necessário.

```
upload_max_filesize = 64M
post_max_size = 50M
memory_limit = 256M
max_execution_time = 60
max_input_time = 60
mysql.connect_timeout = 60
allow_url_fopen = on
allow_url_include = on

date.timezone = "America/Sao_Paulo"
default_charset = UTF-8;
```