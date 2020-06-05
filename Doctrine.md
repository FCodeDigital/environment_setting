# Migrations

Para iniciar um novo projeto ou adicionar novas informações no banco de dados é necessário utilizar o Doctrine Migrations.
Por não ser compatível com o CodeIgniter, foi inserido um projeto por fora.

### Instalando e Configurando o Doctrine

O Doctrine deve ser instalado através do composer, para isso você pode utilizar o seguindo comando no seu terminal:

```
composer global require doctrine/migrations
```

Isso irá instalar o doctrine globalmente e evitará ter que inserir a pasta `vendor` no comando. Caso opte por instalar localmente, pasta rodar o comando `composer install` na raiz do projeto. Nesse caso os comandos seguintes deverão conter o caminho `./../vendor/bin/`.

Em sistemas MAC é necessário adicionar o composer ao `PATH` para utilizar globalmente:

```
export PATH=~/.composer/vendor/bin:$PATH
```

> Em alguns computadores MAC é necessário utilizar a pasta completa nas chamadas `~/.composer/vendor/bin/doctrine-migrations`.

Já em ambientes Windows, é necessário adicionar o caminho `C:\Users\[USER]\AppData\Roaming\Composer\vendor\bin`, para isso procura por "Variáveis de Ambiente" no menu iniciar e altere a variavel `PATH`.

Todos os comandos do Doctrine que serão citados a partir daqui deverão ser executados dentro do diretório `migrations` deste projeto.
É necessário alterar as configurações de conexão com o banco de dados em `migrations/migrations-db.php`, caso não utilize variáveis de ambiente.

### Gerando uma nova migration

Ao gerar uma nova migration será criado um arquivo PHP dento do diretório /lib/Framework/Migrations, onde deverá ser inserido o SQL.
Utilize o seguinte comando para gerar uma nova migration:

```
doctrine-migrations generate
```

## Executando as migrations

Ao executar as migrations o Doctrine irá realizar a atualização das tabelas do banco indicado.
Utilize o seguinte comando para executar as migrations:

```
doctrine-migrations migrate
```

Para mais informações, consulte o [Manual do Doctrine](https://www.doctrine-project.org/projects/doctrine-migrations/en/latest/reference/introduction.html)