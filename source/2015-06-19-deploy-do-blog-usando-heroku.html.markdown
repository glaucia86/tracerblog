---
title: Parte 03 - Deploy da aplicação usando Heroku
date: 2015-06-19 10:20 BRT
tags: blog, middleman
author: Futrica
---

[Parte 01 - Instalar e configurar o Middleman;](/criando-um-blog-com-middleman-pt1.html)<br />
Parte 02 - Desenvolvimento e customização do blog;<br />
Parte 03 - Deploy da aplicação usando Heroku; <br />
Parte 04 - Mantendo e atualizando o blog através de Pull Requests do Github.<br />

Fazer o deploy da aplicação já foi um terrível pesadelo para desenvolvedores, mas graças ao Heroku ficou fácil, rápido e divertido.

Parte 03 - Deploy da aplicação usando Heroku
=================================================

Afinal, o que é o [Heroku](https://www.heroku.com/)? 
Heroku é uma das primeiras plataformas de nuvem , já está em desenvolvimento desde junho de 2007, quando suportava apenas a linguagem de programação Ruby , mas, desde então, adicionou suporte para Java , Node.js , Scala , Clojure e Python e PHP. Com Heroku é possível subir sua aplicação com apenas um comando.
Para isso só precisamos instalar [Heroku toolbelt](https://toolbelt.heroku.com/), ter uma conta heroku e github.

## Preparando a aplicação

Se ainda não inicializou o git, inicie:

```
git init
Initialized empty Git repository in /home/futrica/projects/tracerblog/.git/
$ git add .
$ git commit -m "Initial commit"
```

Para criar uma aplicação no heroku:

```
$ heroku apps:create NOME_DO_SEU_BLOG
```
