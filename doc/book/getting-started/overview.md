# Começando com Aplicações MVC do Zend Framework

Este tutorial destina-se a dar uma introdução ao uso do Zend Framework criando uma aplicação simples com banco de dados usando o paradigma Model-View-Controller. No final você terá uma aplicação ZF funcionando e você poderá então dar uma olhada no código para descobrir mais sobre como tudo funciona e se encaixa.

## Algumas premissas

Este tutorial assume que você está executando ao menos o PHP 5.6 com o servidor
web Apache e MySQL, acessível através da extensão PDO. Sua instalação do Apache
deve ter a extensão `mod_rewrite` instalada e configurada.

Você também deve garantir que o Apache esteja configurado para suportar arquivos `.htaccess`.
Isso geralmente é feito alterando a configuração:

```apache
AllowOverride None
```

para

```apache
AllowOverride FileInfo
```

no seu arquivo `httpd.conf`. Verifique na documentação da sua distribuição para
detalhes exatos. Você não poderá navegar para qualquer outra página além da página
inicial neste tutorial se você não configurou o uso do `mod_rewrite` e
`.htaccess` corretamente.

> ### Começando mais rápido
>
> Por outro lado, você também pode usar qualquer uma das seguintes opções:
>
> - O servidor web interno do PHP. Execute `php -S 0.0.0.0:8080 -t
>   public/index.php` na raiz de sua aplicação para iniciar um servidor web escutando
>   na porta 8080.
> - Use o `Vagrantfile` enviado, executando `vagrant up` a partir da
>   raiz da aplicação. Isso liga a porta 8080 da máquina host à instância do
>   servidor Apache rodando na imagem do Vagrant.
> - Use a integração com o [docker-compose](https://docs.docker.com/compose/)
>   enviada, executando `docker-compose up -d --build` a partir da
>   raiz da aplicação. Isso liga a porta 8080 da máquina host à instância do
>   servidor Apache rodando no container.

## A aplicação do tutorial

A aplicação que iremos construir é um sistema de inventário simples para
exibir os álbuns que possuímos. A página principal listará nossa coleção e nos permitirá
adicionar, editar e deletar CDs. Nós vamos precisar de quatro páginas em nosso website:

Página               | Descrição
-------------------- | -----------
Lista de álbuns      | Esta página exibirá a lista de álbuns e fornecerá links para editá-los e excluí-los. Além disso, um link para permitir a adição de novos álbuns será fornecido.
Adicionar novo álbum | Esta página fornecerá um formulário para adicionar um novo álbum.
Editar álbum         | Esta página fornecerá um formulário para editar um álbum.
Excluir álbum        | Esta página irá confirmará que queremos excluir um álbum e então irá excluí-lo.

Também precisaremos armazenar nossos dados em um banco de dados. Nós só iremos precisar de uma tabela
com estes campos:

Nome do campo | Tipo         | Nulo? | Notas
------------- | ------------ | ----- | -----
id            | integer      | Não   | Primary key, auto-increment
artist        | varchar(100) | Não   |
title         | varchar(100) | Não   |
