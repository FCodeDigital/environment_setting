
## Alterando versão do PHP

Use essas instruções para alterar a versão do PHP nos servidores Locaweb.

A mudança será feita através do arquivo `.htaccess`. Para isso, coloque o seguinte código:
```
<IfModule mime_module>
  AddHandler application/x-httpd-ea-php72 .php .php7 .phtml
</IfModule>
```