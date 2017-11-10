---
layout: post
title:  "Não adicione arquivos do seu SO/editor no .gitignore"
date: 2016-03-06 21:24:11 -0300
categories:
---
A ideia é simples, o arquivo `.gitignore` do projeto deve ser usado somente para ignorar arquivos gerados pelo projeto.

Seu projeto não deve ser responsável por ignorar arquivos gerados pelo seu sistema operacional ou editor por exemplo `.DS_Store`do OS X ou `.idea` das IDEs da JetBrains.

Segundo os [desenvolvedores do Django](https://github.com/django/django/blob/master/.gitignore) por exemplo você deve configurar isso em locais que não vão para o repositório.

Para mim a maneira mais fácil é no `~/.gitconfig` usando o `core.excludesFile`.

Exemplo:

`~/.gitconfig`

    [core]
    excludesFile = ~/.gitignore_global

`~/.gitignore_global`

    *.sublime-project
    *.sublime-workspace
    .idea
    .ipynb_checkpoints

    *.ipynb

    .DS_Store
    Thumbs.db
    desktop.ini

As vantagens são: Você faz isso uma única vez e você não configura o projeto no qual você está trabalhando como responsável por lidar com seus arquivos, que talvez não seja de interesse de outro desenvolvedor, mas que estariam lá caso ele precise dar manutenção no arquivo complicando a vida dele.
