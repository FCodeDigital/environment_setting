# Regras de htaccess no CodeIgniter

As regras padrões do Codeigniter 3 são:

```
RewriteEngine on
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php/$1 [L]
```

### Colocando o site em uma pasta de versão

Caso você queira versionar vários sites em um mesmo ambiente, pode usar as regras abaixo.
Crie uma pasta chamada `/2020` e coloque o conteúdo do site dentro dela.

Dentro da pasta `/2020`, insira o seguinte trecho no `.htaccess`:

```
RewriteEngine on
RewriteBase /
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php?/$1 [L]
```

Na pasta raiz `/`, crie um arquivo `.htaccess` e insira:

```
Options +FollowSymlinks -MultiViews -Indexes

RewriteEngine On
RewriteBase /
```

No mesmo aquivo, se quiser a URL com o nome do diretório (Ex: http://dominio.com.br/2020), use:

```
RewriteCond %{REQUEST_URI}  ^/?$        [NC]
RewriteCond %{REQUEST_URI}  !index\.php [NC]
RewriteRule .*  /NOME_DA_PASTA/  [NC,L]
```

Caso queira deixar transparente, o trecho deve ser:

```
RewriteCond %{REQUEST_URI}  !^/NOME_DA_PASTA     [NC]
RewriteRule ^(.+)  /NOME_DA_PASTA/$1             [NC,L]
```

