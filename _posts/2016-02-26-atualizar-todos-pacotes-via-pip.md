---
layout: post
title:  "Atualizar todos pacotes via pip"
date: 2016-02-26 15:43:41 -0300
categories:
---
Para listar todos os pacotes desatualizados basta usar:

`pip list --outdated`

Então para atualizar tudo de uma vez:

`pip list --outdated | awk '{print $1}' | xargs sudo pip install -U`

Remova o sudo caso queira atualizar dentro do virtualenv.
