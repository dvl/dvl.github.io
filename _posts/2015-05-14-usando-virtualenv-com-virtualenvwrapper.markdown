---
layout: post
title:  "Usando virtualenv com virtualenvwrapper"
date: 2015-05-14 00:17:50 -0300
categories:
---
O uso do `virtualenv` é um item quase que obrigatório em qualquer ambiente de desenvolvimento Python, é usado para isolar os pacotes do projeto dos pacotes do sistema.

O que vejo poucas pessoas usando é o `virtualenvwrapper` que visa a resolver vários problemas criados pelo `virtualenv` como a necessidade de se usar sempre `source bin/activate` e os arquivos do `virtualenv` sendo colocados lado-a-lado com os arquivos do seu projeto.

## Instalação

Primeiro vamos a instalação dos pacotes necessários (essa possivelmente deverá ser a ultima vez que você instala algo globalmente no seu sistema):

    $ sudo pip install virtualenv virtualenvwrapper

E adicione a seguinte linha ao final do seu arquivo `.bashrc` (ou equivalente):

    source /usr/local/bin/virtualenvwrapper.sh

Reinicie seu shell e você possuirá entre outros os seguintes novos comandos.

## Uso

Para criar um novo ambiente use:

     mkvirtualenv meu_projeto

 Para criar um novo ambiente com Python 3:

     mkvirtualenv meu_projeto2 --python=`which python3`

Para listar todos seus ambientes:

    lsvirtualenv

Para executar um comando em todos os ambientes:

    allvirtualenv pip install -U django

E para remover um ambiente:

    rmvirtualenv meu_projeto

E para ativar/trocar de ambiente:

    workon meu_projeto2


Para desativar é igual, sem qualquer novidade:

    deactivate

## Dicas

Caso você esteja usando o `zsh` como shell juntamente com o `oh-my-zsh` é possivel ativar automaticamente um ambiente ao entrar em determinadas pastas (`cd meu_projeto`) para isso adicione o plugin `virtualenvwrapper` a lista de plugins no seu arquivo `.zshrc` e sempre que você entrar em alguma pasta o plugin irá procurar um ambiente com o nome daquela pasta e ativa-lo, também é possivel criar um arquivo chamado `.venv` dentro da pasta do projeto contendo o nome do ambiente a ser ativado (ex.: `echo meu_projeto > .venv`).

Originalmente publicado em: [Python Club](http://www.pythonclub.com.br/)
