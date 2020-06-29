# Regras de htaccess para WWW e HTTPS

As regras abaixo funcionam para redirecionar o domínio e forçar o uso de WWW ou HTTPS.

### Força o uso de `www`:

```
RewriteCond %{HTTP_HOST} !^www\. [NC]
RewriteRule ^(.*)$ http://www.%{HTTP_HOST}/$1 [R=301,L]
```

### Força o uso de www com https (deve ficar na raiz)

```
RewriteEngine on
RewriteBase /

RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteCond %{HTTPS} off
RewriteCond %{HTTP_HOST} !^www\..+$ [NC]
RewriteRule ^ https://www.%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

### Força o uso somente de https (deve ficar na raiz)

```
RewriteEngine on
RewriteBase /

RewriteCond %{HTTP:X-Forwarded-Proto} !https
RewriteCond %{HTTPS} off
RewriteCond %{HTTP_HOST} ^www\.(.+)$ [NC]
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```