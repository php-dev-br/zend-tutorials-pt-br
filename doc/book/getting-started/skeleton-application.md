# Começando: Uma aplicação esqueleto

Para construir a nossa aplicação começaremos com a
[ZendSkeletonApplication](https://github.com/zendframework/ZendSkeletonApplication)
disponível no [github](https://github.com/). Use o [Composer](<http://getcomposer.org>)
para criar um novo projeto do zero:

```bash
$ composer create-project -s dev zendframework/skeleton-application caminho/para/instalar
```

Isso irá instalar um conjunto initial de dependências, incluindo:

- zend-component-installer, que ajuda a automatizar a injeção de configuração de
  componentes na sua aplicação.
- zend-mvc, o kernel para aplicações MVC.

O padrão é fornecer a quantidade mínima de dependências necessárias para executar uma
aplicação zend-mvc. Entretanto, você pode ter necessidades adicionais que você conhece desde
o início, e, assim sendo, o esqueleto também vem com um plugin instalador que
irá fazer a você algumas perguntas.

Primeiro, ele irá perguntar:

```text
    Do you want a minimal install (no optional packages)? Y/n
```

> ### Perguntas e valores padrão
>
> Todas as perguntas feitas pelo instalador fornecem a lista de opções disponíveis
> e irão especificar a opção padrão por meio de uma letra maiúscula. Os valores padrão são
> usados se o usuário pressionar "Enter" sem informar um valor. No exemplo anterior, "Y"
> é o padrão.

Se você responder "Y" ou pressionar "Enter" sem nenhuma seleção o instalador não
fará mais perguntas e irá terminará de instalar a sua aplicação. Se você
responder "n", ele continuará com as perguntas:

```text
    Would you like to install the developer toolbar? y/N
```

A [barra de ferramentas do desenvolvedor](https://github.com/zendframework/ZendDeveloperTools)
fornece uma barra de ferramentas no navegador com informações de tempo e profiling e pode ser
útil ao debugar uma aplicação. Para os fins do tutorial, entretanto,
não iremos usá-la; tecle "Enter" ou "n" seguido de "Enter".

```text
    Would you like to install caching support? y/N
```

Nós não vamos demonstrar o armazenamento em cache neste tutorial, então tecle "Enter" ou
"n" seguido de "Enter".

```text
    Would you like to install database support (installs zend-db)? y/N
```

Nós *iremos* usar zend-db extensivamente neste tutorial, então tecle "y" seguido de
"Enter". Você deve ver o seguinte texto aparecer:

```text
    Will install zendframework/zend-db (^2.8.1)
    When prompted to install as a module, select application.config.php or modules.config.php
```

A próxima pergunta é:

```text
    Would you like to install forms support (installs zend-form)? y/N
```

Este tutorial também usa zend-form, então vamos selecionar novamente "y" para instalá-lo;
ao fazer isso será emitida uma mensagem parecida com aquela emitida para o zend-db.

Neste ponto podemos responder "n" para os seguintes recursos restantes:

```text
    Would you like to install JSON de/serialization support? y/N
    Would you like to install logging support? y/N
    Would you like to install MVC-based console support? (We recommend migrating to zf-console, symfony/console, or Aura.CLI) y/N
    Would you like to install i18n support? y/N
    Would you like to install the official MVC plugins, including PRG support, identity, and flash messages? y/N
    Would you like to use the PSR-7 middleware dispatcher? y/N
    Would you like to install sessions support? y/N
    Would you like to install MVC testing support? y/N
    Would you like to install the zend-di integration for zend-servicemanager? y/N
```

Em um certo ponto você verá o seguinte texto:

```text
Updating root package
    Running an update to install optional packages

...

Updating application configuration...

  Please select which config file you wish to inject 'Zend\Db' into:
  [0] Do not inject
  [1] config/modules.config.php
  Make your selection (default is 0):
```

Queremos habilitar as várias seleções que fizemos na aplicação. Assim sendo,
iremos escolher `1`, o que então nos dará o seguinte prompt:

```text
  Remember this option for other packages of the same type? (y/N)
```

No nosso caso podemos seguramente dizer "y", o que significa que não seremos mais
solicitados a escolher pacotes adicionais. (O único pacote no conjunto padrão de
prompts que você pode não querer habilitar por padrão é `Zend\Test`.)

Uma vez que a instalação esteja concluída o instalador do esqueleto se remove e a
nova aplicação está pronta para começar!

> ### Baixando o esqueleto
>
> Outra forma de instalar a ZendSkeletonApplication é usar o github para
> baixar um arquivo comprimido. Acesse
> https://github.com/zendframework/ZendSkeletonApplication, clique no botão "Clone
> or download" e selecione "Download ZIP". Isso irá baixar um arquivo com um
> nome como `ZendSkeletonApplication-master.zip` ou algo parecido.
>
> Descompacte este arquivo no diretório onde você mantém todos os seus vhosts e renomeie
> o diretório resultante para `zf-tutorial`.
>
> A ZendSkeletonApplication está configurada para usar o [Composer](http://getcomposer.org)
> para resolver suas dependências. Execute o seguinte de dentro da sua nova
> pasta zf-tutorial para instalá-las:
>
> ```bash
> $ composer self-update
> $ composer install
> ```
>
> Isso demora um pouco. Você deve ver uma saída como a seguinte:
>
> ```text
> Installing dependencies from lock file
> - Installing zendframework/zend-component-installer (0.2.0)
>   
> ...
>
> Generating autoload files
> ```
>
> Neste ponto você será solicitado a responder algumas perguntas como mencionado acima.
>
> Por outro lado, se você não tem o Composer instalado mas *tem* o
> Vagrant ou o docker-compose disponível você pode rodar o Composer através deles:
>
> ```bash
> # Para o Vagrant:
> $ vagrant up
> $ vagrant ssh -c 'composer install'
> # Para o docker-compose:
> $ docker-compose build
> $ docker-compose run zf composer install
> ```

> ### Tempos limite
>
> Se você vir esta mensagem:
>
> ```text
> [RuntimeException]      
>   The process timed out.
> ```
>
> então sua conexão estava muito lenta para baixar o pacote inteiro a tempo e
> o composer expirou. Para evitar isso, ao invés de executar:
>
> ```bash
> $ composer install
> ```
>
> execute isso:
>
> ```bash
> $ COMPOSER_PROCESS_TIMEOUT=5000 composer install
> ```

> ### Usuários do Windows usando o WAMP
>
> Para usuários do Windows com o WAMP:
>
> 1. Instale o [composer para o Windows](https://getcomposer.org/doc/00-intro.md#installation-windows).
>    Verifique se o composer está instalado corretamente executando:
>
>    ```bash
>    $ composer
>    ```
>
> 2. Instale o [GitHub Desktop](https://desktop.github.com/) para Windows.
     Verifique se o git está instalado corretamente executando:
>
>    ```bash
>    $ git
>    ```
>
> 3. Agora instale o esqueleto usando:
>
>    ```bash
>    $ composer create-project -s dev zendframework/skeleton-application caminho/para/instalar
>    ```

Agora podemos avançar para a configuração do servidor web.

## Servidores Web

Neste tutorial passaremos por quatro formas diferentes de configurar seu servidor
web:

- Através do servidor web interno do PHP.
- Através do Vagrant.
- Através do docker-compose.
- Usando o Apache.

### Usando o Servidor Web Interno do PHP

Você pode usar o servidor web interno do PHP ao desenvolver sua aplicação. Para fazer
isso inicie o servidor a partir do diretório raiz do projeto:

```bash
$ php -S 0.0.0.0:8080 -t public public/index.php
```

Isso tornará o site disponível na porta 8080 de todas as interfaces de rede,
usando `public/index.php` para lidar com o roteamento. Isso significa que o site está acessível
através de `http://localhost:8080` ou `http://<seu-IP-local>:8080`.

Se você fez tudo certo, você deve ver o seguinte.

![Olá Mundo com o zend-mvc](../images/user-guide.skeleton-application.hello-world.png)

Para testar que o seu roteamento está funcionando acesse `http://localhost:8080/1234`
e você deve ver a seguinte página 404:

![Página 404 do zend-mvc](../images/user-guide.skeleton-application.404.png)

> #### Apenas para Desenvolvimento
>
> O servidor web interno do PHP deve ser usado **apenas para desenvolvimento**.

### Usando o Vagrant

O [Vagrant](https://www.vagrantup.com/) fornece uma maneira de descrever e provisionar
virtual machines, and is a common way to provide a coherent and consistent
development environment for development teams. The skeleton application provides
a `Vagrantfile` based on Ubuntu 14.04, and using the `ondrej/php` PPA to provide
PHP 7.0. Start it up using:

```bash
$ vagrant up
```

Once it has been built and is running, you can also run composer from the
virtual machine. As an example, the following will install dependencies:

```bash
$ vagrant ssh -c 'composer install'
```

while this will update them:

```bash
$ vagrant ssh -c 'composer update'
```

The image uses Apache 2.4, and maps the host port 8080 to port 80 on the virtual
machine.

### Using docker-compose

[Docker](https://www.docker.com/) containers wrap a piece of software and everything needed to run it,
guaranteeing consistent operation regardless of the host environment; it is an
alternative to virtual machines, as it runs as a layer on top of the host
environment.

[docker-compose](https://docs.docker.com/compose/) is a tool for automating
configuration of containers and composing dependencies between them, such as
volume storage, networking, etc.

The skeleton application ships with a `Dockerfile` and configuration for
docker-compose; we recommend using docker-compose, as it provides a foundation
for mapping additional containers you might need as part of your application,
including a database server, cache servers, and more. To build and start the
image, use:

```bash
$ docker-compose up -d --build
```

After the first build, you can truncate this to:

```bash
$ docker-compose up -d
```

Once built, you can also run commands on the container. The docker-compose
configuration initially only defines one container, with the environment name
"zf"; use that to execute commands, such as updating dependencies via composer:

```bash
$ docker-compose run zf composer update
```

The configuration includes both PHP 7.0 and Apache 2.4, and maps the host port
8080 to port 80 of the container.

### Using the Apache Web Server

We will not cover installing [Apache](https://httpd.apache.org), and will assume
you already have it installed. We recommend installing Apache 2.4, and will only
cover configuration for that version.

You now need to create an Apache virtual host for the application and edit your
hosts file so that `http://zf-tutorial.localhost` will serve `index.php` from
the `zf-tutorial/public/` directory.

Setting up the virtual host is usually done within `httpd.conf` or
`extra/httpd-vhosts.conf`. If you are using `httpd-vhosts.conf`, ensure that
this file is included by your main `httpd.conf` file. Some Linux distributions
(ex: Ubuntu) package Apache so that configuration files are stored in
`/etc/apache2` and create one file per virtual host inside folder
`/etc/apache2/sites-enabled`. In this case, you would place the virtual host
block below into the file `/etc/apache2/sites-enabled/zf-tutorial`.

Ensure that `NameVirtualHost` is defined and set to `*:80` or similar, and then
define a virtual host along these lines:

```apache
<VirtualHost *:80>
    ServerName zf-tutorial.localhost
    DocumentRoot /path/to/zf-tutorial/public
    SetEnv APPLICATION_ENV "development"
    <Directory /path/to/zf-tutorial/public>
        DirectoryIndex index.php
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

Make sure that you update your `/etc/hosts` or
`c:\windows\system32\drivers\etc\hosts` file so that `zf-tutorial.localhost` is
mapped to `127.0.0.1`. The website can then be accessed using
`http://zf-tutorial.localhost`.

```none
127.0.0.1 zf-tutorial.localhost localhost
```

Restart Apache.

If you've done so correctly, you will get the same results as covered under
[the PHP built-in web server](#using-the-built-in-php-web-server).

To test that your `.htaccess` file is working, navigate to
`http://zf-tutorial.localhost/1234`, and you should see the 404 page as noted
earlier.  If you see a standard Apache 404 error, then you need to fix your
`.htaccess` usage before continuing.

If you're are using IIS with the URL Rewrite Module, import the following:

```apache
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^ index.php [NC,L]
```

You now have a working skeleton application and we can start adding the specifics for our application.

## Error reporting

Optionally, *when using Apache*, you can use the `APPLICATION_ENV` setting in
your `VirtualHost` to let PHP output all its errors to the browser. This can be
useful during the development of your application.

Edit `zf-tutorial/public/index.php` directory and change it to the following:

```php
<?php

use Zend\Mvc\Application;

/**
 * Display all errors when APPLICATION_ENV is development.
 */
if ($_SERVER['APPLICATION_ENV'] === 'development') {
    error_reporting(E_ALL);
    ini_set("display_errors", 1);
}

/**
 * This makes our life easier when dealing with paths. Everything is relative
 * to the application root now.
 */
chdir(dirname(__DIR__));

// Decline static file requests back to the PHP built-in webserver
if (php_sapi_name() === 'cli-server') {
    $path = realpath(__DIR__ . parse_url($_SERVER['REQUEST_URI'], PHP_URL_PATH));
    if (__FILE__ !== $path && is_file($path)) {
        return false;
    }
    unset($path);
}

// Composer autoloading
include __DIR__ . '/../vendor/autoload.php';

if (! class_exists(Application::class)) {
    throw new RuntimeException(
        "Unable to load application.\n"
        . "- Type `composer install` if you are developing locally.\n"
        . "- Type `vagrant ssh -c 'composer install'` if you are using Vagrant.\n"
        . "- Type `docker-compose run zf composer install` if you are using Docker.\n"
    );
}

// Retrieve configuration
$appConfig = require __DIR__ . '/../config/application.config.php';
if (file_exists(__DIR__ . '/../config/development.config.php')) {
    $appConfig = ArrayUtils::merge($appConfig, require __DIR__ . '/../config/development.config.php');
}

// Run the application!
Application::init($appConfig)->run();
```

## Development mode

Before we begin, we're going to enable *development mode* for the application.
The skeleton application provides two files that allow us to specify general
development settings we want to use everywhere; these may include enabling
modules for debugging, or enabling error display in our view scripts. These
files are located at:

- `config/development.config.php.dist`
- `config/autoload/development.local.php.dist`

When we enable development mode, these files are copied to:

- `config/development.config.php`
- `config/autoload/development.local.php`

This allows them to be merged into our application. When we disable development
mode, these two files that were created are then removed, leaving only the
`.dist` versions. (The repository also contains rules to ignore the copies.)

Let's enable development mode now:

```bash
$ composer development-enable
```

> ### Never enable development mode in production
>
> You should never enable development mode in production, as the typical
> reason to enable it is to enable debugging! As noted, the artifacts generated
> by enabling development mode cannot be committed to your repository, so
> assuming you don't run the command in production, you should be safe.
>
> You can test the status of development mode using:
>
> ```bash
> $ composer development-status
> ```
>
> And you can disable it using:
>
> ```bash
> $ composer development-disable
> ```
