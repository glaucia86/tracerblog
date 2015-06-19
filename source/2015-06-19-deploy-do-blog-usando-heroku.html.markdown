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

Parte 03 - Deploy da aplicação usando Heroku
=================================================

Afinal, o que é o [Heroku](https://www.heroku.com/)? 
Heroku é uma das primeiras plataformas de nuvem , já está em desenvolvimento desde junho de 2007, quando suportava apenas a linguagem de programação Ruby , mas, desde então, adicionou suporte para Java , Node.js , Scala , Clojure e Python e PHP. Com Heroku é possível subir sua aplicação com apenas um comando.
Para isso só precisamos instalar [Heroku toolbelt](https://toolbelt.heroku.com/), ter uma conta heroku e o git.

## Preparando a aplicação

Se ainda não inicializou o repositório git, faça:

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
O comando acima cria uma aplicação no Heroku e também já adiciona um novo remote 
```
Creating NOME_DO_SEU_BLOG.. done, stack is cedar-14
https://NOME_DO_SEU_BLOG.herokuapp.com/ | https://git.heroku.com/NOME_DO_SEU_BLOG.git
Git remote heroku added
```

Agora o que resta é subir a aplicação:

```
git push heroku 
```
Só basta digitar o comando acima que o heroku faz todo o trabalho, cria um máquina, instala todas as dependências da aplicaçã, compila o css e etc … 

           
## Conclusão

O que antes era um pesadelo para desenvolvedores e analistas de infra estrutura, cada vez mais está ficando mais simples, rápido e robusto.

No próximo e último post sobre o tema, veremos como também é fácil manter o blog usando o github.


