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
> Todas as perguntas feitas pelo instalador fornecem a lista de opções disponíveis,
> e irão especificar a opção padrão por meio de uma letra maiúscula. Os valores padrão são
> usados se o usuário pressionar "Enter" sem informar um valor. No exemplo anterior, "Y"
> é o padrão.

Se você responder "Y", ou pressionar "Enter" sem nenhuma seleção, o instalador não
fará mais perguntas e irá terminará de instalar a sua aplicação. Se você
responder "n", ele continuará com as perguntas:

```text
    Would you like to install the developer toolbar? y/N
```

A [barra de ferramentas do desenvolvedor](https://github.com/zendframework/ZendDeveloperTools)
fornece uma barra de ferramentas no navegador com informações de tempo e profiling, e pode ser
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

Neste ponto, podemos responder "n" para os seguintes recursos restantes:

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

Em um determinado ponto, você verá o seguinte texto:

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
iremos escolher `1`, o que então nos dará o seguinte aviso:

```text
  Remember this option for other packages of the same type? (y/N)
```

Em nosso caso, podemos seguramente dizer "y", o que significa que não seremos mais
solicitados a escolher pacotes adicionais. (O único pacote no conjunto padrão de
perguntas que você pode não querer habilitar por padrão é `Zend\Test`.)

Uma vez que a instalação esteja concluída, o instalador do esqueleto irá se remover, e a
nova aplicação está pronta para começar!

> ### Baixando o esqueleto
>
> Outra forma de instalar a ZendSkeletonApplication é usar o github para
> baixar um arquivo comprimido. Acesse
> https://github.com/zendframework/ZendSkeletonApplication, clique no botão "Clone
> or download", e selecione "Download ZIP". Isso irá baixar um arquivo com um
> nome como `ZendSkeletonApplication-master.zip` ou algo parecido.
>
> Descompacte este arquivo no diretório onde você mantém todos os seus vhosts e renomeie
> o diretório resultante para `tutorial-zf`.
>
> A ZendSkeletonApplication está configurada para usar o [Composer](http://getcomposer.org)
> para resolver suas dependências. Execute o seguinte de dentro da sua nova
> pasta tutorial-zf para instalá-las:
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
> Neste ponto, você será solicitado a responder algumas perguntas como mencionado acima.
>
> Por outro lado, se você não tem o Composer instalado, mas *tem* o
> Vagrant ou o docker-compose disponível, você pode executar o Composer através deles:
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
> Se você ver esta mensagem:
>
> ```text
> [RuntimeException]      
>   The process timed out.
> ```
>
> então sua conexão estava muito lenta para baixar o pacote inteiro a tempo, e
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

Neste tutorial, passaremos por quatro formas diferentes de configurar seu servidor
web:

- Através do servidor web interno do PHP.
- Através do Vagrant.
- Através do docker-compose.
- Usando o Apache.

### Usando o Servidor Web Interno do PHP

Você pode usar o servidor web interno do PHP ao desenvolver sua aplicação. Para fazer
isso, inicie o servidor a partir do diretório raiz do projeto:

```bash
$ php -S 0.0.0.0:8080 -t public public/index.php
```

Isso tornará o site disponível na porta 8080 de todas as interfaces de rede,
usando `public/index.php` para lidar com o roteamento. Isso significa que o site estará acessível
através de `http://localhost:8080` ou `http://<seu-IP-local>:8080`.

Se você fez isso direito, você deve ver o seguinte:

![Olá, Mundo com o zend-mvc](../images/user-guide.skeleton-application.hello-world.png)

Para testar que o seu roteamento está funcionando, acesse `http://localhost:8080/1234`,
e você deve ver a seguinte página 404:

![Página 404 do zend-mvc](../images/user-guide.skeleton-application.404.png)

> #### Apenas para desenvolvimento
>
> O servidor web interno do PHP deve ser usado **apenas para desenvolvimento**.

### Usando o Vagrant

O [Vagrant](https://www.vagrantup.com/) fornece uma maneira de descrever e provisionar
máquinas virtuais, e é uma maneira comum de fornecer um ambiente de desenvolvimento
coerente e consistente para as equipes de desenvolvimento. A aplicação esqueleto fornece
um `Vagrantfile` baseado no Ubuntu 14.04, e usa o PPA `ondrej/php` para fornecer o
PHP 7.0. Inicie o Vagrant usando:

```bash
$ vagrant up
```

Uma vez que ele tenha sido construído e esteja rodando, você poderá também executar o composer a partir da
máquina virtual. Como exemplo, o seguinte comando irá instalar as dependências:

```bash
$ vagrant ssh -c 'composer install'
```

enquanto este irá atualizá-las:

```bash
$ vagrant ssh -c 'composer update'
```

A imagem usa o Apache 2.4, e mapeia a porta 8080 do host para a porta 80 na máquina
virtual.

### Usando o docker-compose

Os containers do [Docker](https://www.docker.com/) empacotam uma porção de software e tudo o que é necessário para executá-lo,
garantindo uma operação consistente independentemente do ambiente do host; o Docker é uma
alternativa às máquinas virtuais, pois é executado como uma camada em cima do ambiente do
host.

O [docker-compose](https://docs.docker.com/compose/) é uma ferramenta para automatizar
a configuração de containers e compor as dependências entre eles, como
armazenamento de volume, rede, etc.

A aplicação esqueleto vem com um `Dockerfile` e configuração para o
docker-compose; recomendamos usar o docker-compose, pois ele fornece uma base
para mapear containers adicionais que você possa precisar como parte de sua aplicação,
incluindo um servidor de banco de dados, servidores de cache, entre outros. Para construir a imagem e iniciar os
containers, use:

```bash
$ docker-compose up -d --build
```

Depois da primeira construção, você pode reduzir o comando para:

```bash
$ docker-compose up -d
```

Uma vez construída a imagem, você também pode executar comandos no container. A configuração
do docker-compose inicialmente define apenas um container, com o nome de ambiente
"zf"; use-o para executar comandos, como atualizar dependências via composer:

```bash
$ docker-compose run zf composer update
```

A configuração inclui o PHP 7.0 e o Apache 2.4, e mapeia a porta 8080 do
host para a porta 80 do container.

### Usando o Servidor Web Apache

Não abordaremos a instalação do [Apache](https://httpd.apache.org), e assumiremos
que você já o tenha instalado. Recomendamos instalar o Apache 2.4, e iremos cobrir
apenas a configuração para esta versão.

Agora você precisa criar um virtual host no Apache para a aplicação e editar seu
arquivo de hosts para que `http://tutorial-zf.localhost` sirva o `index.php` do
diretório `tutorial-zf/public/`.

A configuração do virtual host geralmente é feita no `httpd.conf` ou em
`extra/httpd-vhosts.conf`. Se você está usando `httpd-vhosts.conf`, verifique se
este arquivo está incluído no seu arquivo principal `httpd.conf`. Algumas distribuições Linux
(ex: Ubuntu) empacotam o Apache de forma que os arquivos de configuração sejam armazenados em
`/etc/apache2` e criam um arquivo para cada virtual host dentro da pasta
`/etc/apache2/sites-enabled`. Neste caso, você colocaria o bloco de virtual
host abaixo no arquivo `/etc/apache2/sites-enabled/tutorial-zf`.

Certifique-se de que `NameVirtualHost` está definido como `*:80` ou algo parecido, e então
defina um virtual host como esse:

```apache
<VirtualHost *:80>
    ServerName tutorial-zf.localhost
    DocumentRoot /caminho/para/tutorial-zf/public
    SetEnv APPLICATION_ENV "development"
    <Directory /caminho/para/tutorial-zf/public>
        DirectoryIndex index.php
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

Certifique-se de atualizar seu arquivo `/etc/hosts` ou
`c:\windows\system32\drivers\etc\hosts` para que `tutorial-zf.localhost` seja
mapeado para `127.0.0.1`. O site pode então ser acessado usando
`http://tutorial-zf.localhost`.

```none
127.0.0.1 tutorial-zf.localhost localhost
```

Reinicie o Apache.

Se você fez isso de forma correta, você terá os mesmos resultados mostrados com
[o servidor web interno do PHP](#usando-o-servidor-web-interno-do-php).

Para testar que o seu arquivo `.htaccess` está funcionando, acesse
`http://tutorial-zf.localhost/1234`, e você deve ver a página 404 como mencionado
anteriormente. Se você ver um erro 404 padrão do Apache, então você precisa corrigir o
seu `.htaccess` antes de continuar.

Se você estiver usando o IIS com o módulo URL Rewrite, importe o seguinte:

```apache
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^ index.php [NC,L]
```

Você agora possui uma aplicação esqueleto funcionando e podemos começar a adicionar os detalhes da nossa aplicação.

## Relatório de erros

Opcionalmente, *ao usar o Apache*, você pode usar a configuração `APPLICATION_ENV` no
seu `VirtualHost` para permitir que o PHP envie todos os seus erros para o navegador. Isso pode ser
útil durante o desenvolvimento da sua aplicação.

Edite o arquivo `tutorial-zf/public/index.php` e altere-o para o seguinte:

```php
<?php

use Zend\Mvc\Application;

/**
 * Exibir todos os erros quando o valor de APPLICATION_ENV é development.
 */
if ($_SERVER['APPLICATION_ENV'] === 'development') {
    error_reporting(E_ALL);
    ini_set("display_errors", 1);
}

/**
 * Isso torna nossa vida mais fácil ao lidar com caminhos. Tudo é relativo
 * à raiz da aplicação agora.
 */
chdir(dirname(__DIR__));

// Recusar requisições de arquivos estáticos ao servidor web interno do PHP
if (php_sapi_name() === 'cli-server') {
    $path = realpath(__DIR__ . parse_url($_SERVER['REQUEST_URI'], PHP_URL_PATH));
    if (__FILE__ !== $path && is_file($path)) {
        return false;
    }
    unset($path);
}

// Autoloading do Composer
include __DIR__ . '/../vendor/autoload.php';

if (! class_exists(Application::class)) {
    throw new RuntimeException(
        "Não é possível carregar a aplicação.\n"
        . "- Digite `composer install` se você estiver desenvolvendo localmente.\n"
        . "- Digite `vagrant ssh -c 'composer install'` se você estiver usando o Vagrant.\n"
        . "- Digite `docker-compose run zf composer install` se você estiver usando o Docker.\n"
    );
}

// Carrega a configuração
$appConfig = require __DIR__ . '/../config/application.config.php';
if (file_exists(__DIR__ . '/../config/development.config.php')) {
    $appConfig = ArrayUtils::merge($appConfig, require __DIR__ . '/../config/development.config.php');
}

// Executa a aplicação!
Application::init($appConfig)->run();
```

## Modo de desenvolvimento

Antes de começarmos, vamos habilitar o *modo de desenvolvimento* para a aplicação.
A aplicação esqueleto fornece dois arquivos que nos permitem especificar configurações
gerais de desenvolvimento que queremos usar em todos os lugares; estas podem incluir habilitar
módulos para depuração, ou habilitar a exibição de erros em nossos view scripts. Estes
arquivos estão localizados em:

- `config/development.config.php.dist`
- `config/autoload/development.local.php.dist`

Quando habilitamos o modo de desenvolvimento, estes arquivos são copiados para:

- `config/development.config.php`
- `config/autoload/development.local.php`

Isso permite que eles sejam incorporados na nossa aplicação. Quando desabilitamos o modo de
desenvolvimento, estes dois arquivos que foram criados são então removidos, deixando apenas as
versões `.dist`. (O repositório também contém regras para ignorar as cópias.)

Agora vamos habilitar o modo de desenvolvimento:

```bash
$ composer development-enable
```

> ### Nunca habilite o modo de desenvolvimento em produção
>
> Você nunca deve habilitar o modo de desenvolvimento em produção, pois a razão
> típica para habilitá-lo é para habilitar a depuração! Conforme observado, os artefatos gerados
> ao habilitar o modo de desenvolvimento não podem ser enviados para o seu repositório, então
> desde que você não execute o comando em produção, você deve estar seguro.
>
> Você pode testar o status do modo de desenvolvimento usando:
>
> ```bash
> $ composer development-status
> ```
>
> E você pode desabilitá-lo usando:
>
> ```bash
> $ composer development-disable
> ```
