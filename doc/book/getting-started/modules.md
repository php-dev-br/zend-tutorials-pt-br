# Módulos

O zend-mvc usa um sistema de módulos para organizar seu código específico da aplicação
principal dentro de cada módulo. O módulo `Application` fornecido pelo esqueleto é usado
para fornecer configuração de bootstrapping, erro e roteamento para toda a
aplicação. Ele geralmente é usado para fornecer controllers a nível de aplicação para
a página inicial de uma aplicação, mas não vamos usar o padrão
fornecido neste tutorial, pois queremos que nossa lista de álbuns seja a página inicial,
que ficará em nosso próprio módulo.

Vamos colocar todo o nosso código no módulo `Album`, que irá conter nossos
controllers, models, forms e views, juntamente com a configuração. Também ajustaremos
o módulo `Application` conforme necessário.

Vamos começar com os diretórios necessários.

## Configurando o módulo Album

Comece criando um diretório chamado `Album` em `module` com os seguintes
subdiretórios para manter os arquivos do módulo:

```text
tutorial-zf/
    /module
        /Album
            /config
            /src
                /Controller
                /Form
                /Model
            /view
                /album
                    /album
```

O módulo `Album` possui diretórios separados para os diferentes tipos de arquivos que
teremos. Os arquivos PHP que contêm classes dentro do namespace `Album` ficam
no diretório `src/`. O diretório `view` também tem uma sub-pasta chamada `album`
para os view scripts do nosso módulo.

Para carregar e configurar um módulo, o Zend Framework fornece um
`ModuleManager`. Este irá procurar por uma classe `Module` no namespace do módulo
especificado (ou seja, `Album`); no caso do nosso novo módulo, isso significa a classe
`Album\Module`, que será encontrada em `module/Album/src/Module.php`.

Vamos criar esse arquivo agora, com o seguinte conteúdo:

```php
namespace Album;

use Zend\ModuleManager\Feature\ConfigProviderInterface;

class Module implements ConfigProviderInterface
{
    public function getConfig()
    {
        return include __DIR__ . '/../config/module.config.php';
    }
}
```

O `ModuleManager` chamará `getConfig()` automaticamente para nós.

### Autoloading

Embora o Zend Framework forneça recursos de autoloading através do seu
componente [zend-loader](https://zendframework.github.io/zend-loader),
recomendamos o uso dos recursos de autoloading do Composer. Assim sendo, precisamos informar
ao Composer nosso novo namespace, e onde seus arquivos ficam.

Abra o `composer.json` na raiz do seu projeto, e procure a seção `autoload`;
ela deve parecer o seguinte por padrão:

```json
"autoload": {
    "psr-4": {
        "Application\\": "module/Application/src/"
    }
},
```

Agora vamos adicionar o nosso novo módulo à lista, então agora a seção é lida assim:

```json
"autoload": {
    "psr-4": {
        "Application\\": "module/Application/src/",
        "Album\\": "module/Album/src/"
    }
},
```

Depois de fazer essa alteração, execute o seguinte comando para garantir que o Composer atualize suas
regras de autoloading:

```bash
$ composer dump-autoload
```

## Configuração

Tendo registrado o autoloader, vamos dar uma olhada no método `getConfig()`
em `Album\Module`. Este método carrega o arquivo `config/module.config.php`
no diretório raiz do módulo.

Crie um arquivo chamado `module.config.php` em
`tutorial-zf/module/Album/config/`:

```php
namespace Album;

use Zend\ServiceManager\Factory\InvokableFactory;

return [
    'controllers' => [
        'factories' => [
            Controller\AlbumController::class => InvokableFactory::class,
        ],
    ],
    'view_manager' => [
        'template_path_stack' => [
            'album' => __DIR__ . '/../view',
        ],
    ],
];
```

A informação de configuração é passada para os componentes relevantes pelo
`ServiceManager`. Precisamos de duas seções iniciais: `controllers` e
`view_manager`. A seção `controllers` fornece uma lista de todos os controllers
fornecidos pelo módulo. Nós precisaremos de um controller, `AlbumController`; iremos
referenciá-lo pelo seu nome de classe totalmente qualificado, e usaremos a `InvokableFactory`
do zend-servicemanager para criar instâncias dele.

Na seção `view_manager`, adicionamos nosso diretório de view à
configuração `TemplatePathStack`. Isso permitirá que ele encontre os view scripts
do módulo `Album` que estão armazenados em nosso diretório `view/`.

## Informando a aplicação sobre nosso novo módulo

Agora precisamos dizer ao `ModuleManager` que este novo módulo existe. Isso é
feito no arquivo `config/modules.config.php` da aplicação, que é fornecido
pela aplicação esqueleto. Atualize este arquivo para que o array que ele retorna
também contenha o módulo `Album`, então o arquivo agora parece com isso:

(As alterações necessárias estão destacadas usando comentários; os comentários originais do
arquivo foram omitidos por brevidade.)

```php
return [
    'Zend\Form',
    'Zend\Db',
    'Zend\Router',
    'Zend\Validator',
    'Application',
    'Album',          // <-- Adicione esta linha
];
```

Como você pode ver, adicionamos nosso módulo `Album` na lista de módulos após
o módulo `Application`.

Agora deixamos o módulo configurado, pronto para colocar nosso código personalizado nele.
