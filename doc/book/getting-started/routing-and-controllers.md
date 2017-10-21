# Roteamento e Controllers

Nós iremos construir um sistema de inventário bem simples para exibir a nossa coleção de álbuns.
A página inicial listará nossa coleção e nos permitirá adicionar, editar e excluir
álbuns. Por isso, as seguintes páginas são necessárias:

Página               | Descrição
-------------------- | -----------
Home                 | Esta página exibirá a lista de álbuns e fornecerá links para editá-los e excluí-los. Além disso, um link para permitir a adição de novos álbuns será fornecido.
Adicionar novo álbum | Esta página fornecerá um formulário para adicionar um novo álbum.
Editar álbum         | Esta página fornecerá um formulário para editar um álbum.
Excluir álbum        | Esta página irá confirmar que queremos excluir um álbum e então irá excluí-lo.

Antes de configurar nossos arquivos, é importante entender como o framework
espera que as páginas sejam organizadas. Cada página da aplicação é conhecida como uma
*action* e actions são agrupadas em *controllers* dentro de *módulos*. Assim, você
geralmente agruparia actions relacionadas em um controller; por exemplo, um controller
de notícia pode ter as actions `atual`, `arquivadas` e `exibir`.

Como temos quatro páginas que se aplicam a álbuns, as agruparemos em um único
controller `AlbumController` dentro do nosso módulo `Album` como quatro actions. As quatro
actions serão:

Página               | Controller        | Action
-------------------- | ----------------- | ------
Home                 | `AlbumController` | `index`
Adicionar novo álbum | `AlbumController` | `add`
Editar álbum         | `AlbumController` | `edit`
Excluir álbum        | `AlbumController` | `delete`

O mapeamento de um URL para uma action específica é feito usando rotas que são
definidas no arquivo `module.config.php` do módulo. Iremos adicionar uma rota para nossas
actions de álbum. Este é o arquivo de configuração do módulo atualizado com o novo código
destacado com comentários:

```php
namespace Album;

use Zend\Router\Http\Segment;
use Zend\ServiceManager\Factory\InvokableFactory;

return [
    'controllers' => [
        'factories' => [
            Controller\AlbumController::class => InvokableFactory::class,
        ],
    ],

    // A seção a seguir é nova e deve ser adicionada ao seu arquivo:
    'router' => [
        'routes' => [
            'album' => [
                'type'    => Segment::class,
                'options' => [
                    'route' => '/album[/:action[/:id]]',
                    'constraints' => [
                        'action' => '[a-zA-Z][a-zA-Z0-9_-]*',
                        'id'     => '[0-9]+',
                    ],
                    'defaults' => [
                        'controller' => Controller\AlbumController::class,
                        'action'     => 'index',
                    ],
                ],
            ],
        ],
    ],

    'view_manager' => [
        'template_path_stack' => [
            'album' => __DIR__ . '/../view',
        ],
    ],
];
```

O nome da rota é 'album' e tem um tipo de 'segment'. Rotas de segmento
nos permitem especificar espaços reservados no padrão do URL (rota) que serão mapeados
para parâmetros nomeados na rota casada. Neste caso, a rota é
**`/album[/:action[/:id]]`** e irá casar com qualquer URL que comece com `/album`.
O próximo segmento será um nome de action opcional e, finalmente, o próximo
segmento será mapeado para um ID opcional. Os colchetes indicam que um
segmento é opcional. A seção constraints nos permite garantir que os
caracteres dentro de um segmento são como esperados, então nós temos actions limitadas a
começar com uma letra e então caracteres subseqüentes sendo apenas alfanuméricos,
sublinhados ou hífens. Também limitamos o ID a apenas dígitos.

Esta rota nos permite ter os seguintes URLs:

URL               | Página                     | Action
----------------- | -------------------------- | ------
`/album`          | Home (lista de álbuns)     | `index`
`/album/add`      | Adicionar novo álbum       | `add`
`/album/edit/2`   | Editar o álbum com o ID 2  | `edit`
`/album/delete/4` | Excluir o álbum com o ID 4 | `delete`

### Crie o controller

Agora estamos prontos para configurar nosso controller. Para o zend-mvc, o controller
é uma classe que é geralmente chamada `{Nome do Controller}Controller`; note que
`{Nome do Controller}` deve começar com uma letra maiúscula. Essa classe fica em um arquivo
chamado `{Nome do Controller}Controller.php` dentro do subdiretório `Controller` do
módulo; no nosso caso é `module/Album/src/Controller/`. Cada action
é um método público dentro da classe controller que é nomeado `{nome da
action}Action`, onde `{nome da action}` deve começar com uma letra
minúscula.

> #### Convenções não aplicadas estritamente
>
> Isto é por convenção. O zend-mvc não oferece muitas restrições aos
> controllers além de que eles devem implementar a interface `Zend\Stdlib\Dispatchable`.
> O framework fornece duas classes abstratas que fazem isso por nós:
> `Zend\Mvc\Controller\AbstractActionController` e
> `Zend\Mvc\Controller\AbstractRestfulController`. Iremos usar o padrão
> `AbstractActionController`, mas se você pretende escrever um serviço web
> RESTful, `AbstractRestfulController` pode ser útil.

Vamos seguir em frente e criar nossa classe controller no arquivo
`tutorial-zf/module/Album/src/Controller/AlbumController.php`:

```php
namespace Album\Controller;

use Zend\Mvc\Controller\AbstractActionController;
use Zend\View\Model\ViewModel;

class AlbumController extends AbstractActionController
{
    public function indexAction()
    {
    }

    public function addAction()
    {
    }

    public function editAction()
    {
    }

    public function deleteAction()
    {
    }
}
```

Agora criamos as quatro actions que queremos usar. Elas não irão funcionar ainda
até que configuremos as views. Os URLs para cada action são:

URL                                         | Método chamado
------------------------------------------- | -------------
`http://tutorial-zf.localhost/album`        | `Album\Controller\AlbumController::indexAction`
`http://tutorial-zf.localhost/album/add`    | `Album\Controller\AlbumController::addAction`
`http://tutorial-zf.localhost/album/edit`   | `Album\Controller\AlbumController::editAction`
`http://tutorial-zf.localhost/album/delete` | `Album\Controller\AlbumController::deleteAction`

Agora temos um router funcionando e as actions estão configuradas para cada página da nossa
aplicação.

É hora de construir a camada da view e do model.

## Inicialize os view scripts

Para integrar a view em nossa aplicação, precisamos criar alguns arquivos de view
script. Esses arquivos serão executados pela `DefaultViewStrategy` e lhes serão
passadas quaisquer variáveis ou view models que sejam retornados do método action do
controller. Esses view scripts são armazenados no diretório views do nosso módulo dentro de um
diretório com o nome do controller. Crie esses quatro arquivos vazios agora:

- `module/Album/view/album/album/index.phtml`
- `module/Album/view/album/album/add.phtml`
- `module/Album/view/album/album/edit.phtml`
- `module/Album/view/album/album/delete.phtml`

Agora podemos começar a preencher tudo, começando com nosso banco de dados e models.
