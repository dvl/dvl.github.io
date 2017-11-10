---
layout: post
title:  "Django - melhorando a estrutura inicial do projeto"
date: 2016-09-03 19:28:42 -0300
categories:
---
Creio que por razões históricas a equipe do Django nunca se preocupou muito em alterar a disposição de arquivos e pastas que tanto os comandos `startproject` e `startapp` geram.

Na minha opinião ambos tem um problema muito sério que é não criar um namespace exclusivo para o seu projeto.

> Namespaces are one honking great idea -- let's do more of those!

> The Zen of Python, by Tim Peters

Na estrutura padrão é muito normal que você termine importações parecidas com:

    from filmes.models import Titulo
    from series.models import Ator

Entretanto isso na minha cabeça gera uma ambiguidade enorme, seriam filmes e series parte do projeto? Seriam da biblioteca padrão? Seriam pacotes baixados do PyPi? Pelo nome posso dizer que fazem parte do projeto mas nem sempre é tão simples assim.

O próprio Django usa namespace, você não faz:

    from utils import timezone
    from utils.crypto import get_random_string

E sim:

    from django.utils import timezone
    from django.utils.crypto import get_random_string

Então porque com nosso projeto não podemos fazer semelhante?

    from philos.filmes.models import Titulo
    from philos.series.models import Ator

Esse é um padrão bem simples de ser implementado no seu projeto Django, vamos a um exemplo, logo após o `startproject` nossa estrutura de diretórios é idêntica a exibida abaixo.

    philos.tv
    ├── manage.py
    └── philos
        ├── __init__.py
        ├── settings.py
        ├── urls.py
        └── wsgi.py

Ao criar uma nova app ele por padrão é colocado na raiz do projeto, nesse caso precisamos mover essa nova app no nosso caso para dentro da pasta `philos` ficando da seguinte forma:

    philos.tv
    ├── manage.py
    └── philos
        ├── filmes
        │   ├── admin.py
        │   ├── apps.py
        │   ├── __init__.py
        │   ├── migrations
        │   │   └── __init__.py
        │   ├── models.py
        │   ├── tests.py
        │   └── views.py
        ├── __init__.py
        ├── settings.py
        ├── urls.py
        └── wsgi.py

Para facilitar isso pode ser feito com os seguintes comandos:

    $ mkdir -p philos/filmes
    $ python manage.py startapp filmes philos/filmes

Então registramos nossa app no `settings.py` da seguinte forma:

    INSTALLED_APPS = [
        'django.contrib.admin',
        ...
        'philos.filmes',
    ]

Criei um [repositório no GitHub](https://github.com/dvl/example-for-blog-1) para que você possa navegar pelas pastas para facilitar o entendimento.

Também tenho um [outro projeto](https://github.com/dvl/cookiecutter-django-clean-template) que uso de base para qualquer projeto que começo atualmente.
