---
title: criando-um-blog-com-middleman-pt2
date: 2015-02-24 15:30 BRT
tags: blog, middleman
author: Futrica
---

Parte 01 - Instalar e configurar o Middleman;
[Parte 02 - Desenvolvimento e customização do blog;](/criando-um-blog-com-middleman-pt1)
Parte 03 - Deploy da aplicação usando Heroku; 
Parte 04 - Mantendo e atualizando o blog através de Pull Requests do Github.

Continuando com a o tema de Criação de blog com Middleman … 

Parte 02 - Desenvolvimento e customização do blog
========================================

Agora que já temos nosso post criado `source/2015-02-23-exemplo-post.html.markdown` e toda a estrutura de links criados. Vamos começar a configurar o layout do site, que podemos ver que está bem poluída:

![blog](/images/index.png "blog poluído!")

 ** Não é intenção entrarmos em detalhes na aparência e layout do site, vamos implementar o somente mínimo para deixar “cada coisa em seu lugar”.

## Configurando o layout do Blog

Essas alterações devem ser feitas no arquivo, `source/layout.rb` é lá que é setada a configuração padrão do seu site / blog.
Podemos ver que está trazendo muita informação para a a página inicial, como: 

Pots recentes:

```erb
<h2>Recent Articles</h2>
<% blog.articles[0...10].each do |article| %>
  ... 
  <% end %>
  ```

  Posts por Tags:

  ```erb
  <h2>Tags</h2>
  <% blog.tags.each do |tag, articles| %>
    ...
    <% end %>
    ```

    Posts por ano:

    ```erb
    <h2>By Year</h2>
    <% blog.articles.group_by {|a| a.date.year }.each do |year, articles| %>
      ...
      <% end %>
      ```





