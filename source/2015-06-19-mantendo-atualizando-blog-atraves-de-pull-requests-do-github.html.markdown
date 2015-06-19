---
title: Parte 04 - Mantendo o blog com Github.
date: 2015-06-19 11:07 BRT
tags: blog, middleman
author: Futrica
---

[Parte 01 - Instalar e configurar o Middleman;](/criando-um-blog-com-middleman-pt1.html)<br />
Parte 02 - Desenvolvimento e customização do blog;<br />
Parte 03 - Deploy da aplicação usando Heroku; <br />
Parte 04 - Mantendo o blog com Github.<br />

A proposta é mostrar como manter e atualizar o blog usando Pull Request do github.

Parte 04 - Mantendo e atualizando o blog através de Pull Requests do Github.
=================================================

A ideia é ter uma nova branch para cada novo post.
Para criar a branch:

```
$ git branch novo-post
```

e para mudar para nova branch criada:

```
$ git checkout novo-post
```

vamos criar um novo post somente para teste:

```
$ middleman article novo-post
      create  source/2015-06-19-novo-post.html.markdown
```

Adicione conteúdo ao post e ...

##  Abrindo um PR no github

Primeiro, vamos adicionar o que criamos de novo e commitar as mudanças:

```
$ git add .
$ git commit -m "novo post para o blog"
[novo-post 3011ae8] novo post para o blog
 1 file changed, 6 insertions(+)
 create mode 100644 source/2015-06-19-novo-post.html.markdown
```

Subir as alterações realizadas nessa branch:

```
$ git push origin novo-post
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 408 bytes | 0 bytes/s, done.
Total 4 (delta 2), reused 0 (delta 0)
To git@github.com:futrica/exemplo_blog.git
 * [new branch]      novo-post -> novo-post
```

![alt text](/images/branch.png "branch")

Depois de subir basta clicar no botão "Compare & pull request" para criar um novo PR.

![alt text](/images/pr.png "criando PR")

E temos a página de PR.

![alt text](/images/pr-page.png "Página de PR")

O post fica aberto pra ser revisado por todos e quando estiver tudo Ok, basta
fazer o merge com o master, usando o botão "Merge pull request".

Pronto basta mudar para branch master e subir a aplicação com heroku.

```
$ git checkout master
$ git push heroku master
```

## Conclusão

Ao longo desses 4 postsm tentamos passar com é bem simples criar e manter um blog usando a combinação:
Ruby + gem Middleman + Heroku.
As ferramentas acima fazem todo trabalho e você foca somente no conteúdo.

## Bônus - Deploy automático

Você pode configurar o Heroku para "monitorar" o github e informar qual branch
ele deve fazer o deploy automático.
Para isso basta acessar o site do Heroku, fazer login, acessar a página do aplicativo
criada, acessar a aba "Deploy" e conectar com github:

![alt text](/images/github-conect.png "conectar com github")

Uma vez conectado, basta ativar o deploy automático:

![alt text](/images/automatic-deploy.png "deploy automático")

Pronto! Agora toda push feito na branch master ou merge com a master, automaticamente
é "pushado" pro Heroku também.

