---
title: Criando um blog com middleman - Parte 02
date: 2015-02-24 18:10 BRT
tags: blog, middleman
author: Futrica
---

[Parte 01 - Instalar e configurar o Middleman;](/criando-um-blog-com-middleman-pt1.html)<br />
Parte 02 - Desenvolvimento e customização do blog;<br />
Parte 03 - Deploy da aplicação usando Heroku; <br />
Parte 04 - Mantendo e atualizando o blog através de Pull Requests do Github.<br />

Continuando com a o tema de Criação de blog com Middleman, vamos implementar as 
views para as páginas: index, tags e post, retirando elementos desnecessários
e trazendo os elementos que queremos mostrar.


Parte 02 - Desenvolvimento e customização do blog
=================================================


Agora que já temos nosso post criado `source/2015-02-23-exemplo-post.html.markdown` e toda a estrutura de links criados. Vamos começar a configurar o layout do site, que como podemos ver, está bem poluída:

![blog](/images/blog.png "blog poluído!")

** Não é intenção entrarmos em detalhes na aparência (CSS) do site, vamos implementar o somente mínimo para deixar “cada coisa em seu lugar”.

## Configurando o layout do Blog

Essas alterações devem ser feitas no arquivo, `source/layout.rb` onde é setada a visualização padrão do seu site / blog.
Podemos ver que está trazendo muita informação, como: 

Posts recentes, por tags, por ano e etc ...:

```erb
<% blog.articles[0...10].each do |article| %>
  ... 
<% end %>

<% blog.tags.each do |tag, articles| %>
    ...
<% end %>

<% blog.articles.group_by {|a| a.date.year }.each do |year, articles| %>
  ...
<% end %>
```
Vamos deixar o layout mais limpo e criar views específicas para o topo da página e rodapé.


## Criando partials

Partial é um "pedaço" de página que pode ser reutilizada em outra página, 
cumprindo assim o princípio [DRY](http://pt.wikipedia.org/wiki/Ruby_on_Rails#DRY).
Crie dois arquivo com as seguintes configurações:

```erb
#source/_nav.html.erb
<header>
  topo
</header>
```
```erb
#source/_footer.html.erb
<footer>
  rodapé
</footer>
```

Agora podemos "limpar" nosso layout: 

`source/layout.erb`

```erb
<!doctype html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta http-equiv='X-UA-Compatible' content='IE=edge;chrome=1' />
    <title>Blog Title<%= ' - ' + current_article.title unless current_article.nil? %></title>
    <%= feed_tag :atom, "#{blog.options.prefix.to_s}/feed.xml", title: "Atom Feed" %>
    <%= stylesheet_link_tag "blog" %>
  </head>
  <body>
    <div class="all">
      <%= partial 'nav' %>
      <%= yield %>
      <%= partial 'footer' %>
    </div>
  </body>
</html>

```

Adicione também um arquivo básico CSS para visualizarmos melhor a estrutura da página:

`#source/stylesheets/blog.css`

```css
.all{
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  width: 800px;
}

header, footer{
  background-color: lightblue;
  padding: 50px
}

article{
  margin: 30px;
}
```
Agora ficamos com o topo, rodapé e o conteúdo. Esse layout é aplicado por padrão a todas as páginas do blog.

## Alterando as configurações do blog

A ideia é agrupar os posts por TAGS, para facilitar a visualização do conteúdo.
O arquivo de configuração do blog `config.rb` é auto explicativo. Vamos deixá-lo de 
acordo com nossa necessidade no momento:

```rb
Time.zone = "Brasilia" # setando time zone

activate :blog do |blog|
  blog.permalink = "{year}/{month}/{day}/{title}.html" #mostra a página do post com data
  blog.taglink = "tags/{tag}.html" # adiciona a função de agrupamento por tags
  blog.layout = "layout" #arquivo padrão do layout
  blog.summary_length = 250 #ativa sumário para o post - requerido gem Nokogiri
  blog.default_extension = ".markdown" # linguagem de marcação dinâmica

  blog.tag_template = "tag.html" #layout específico para página tags

  #Ativar paginação 
  blog.paginate = true
  blog.per_page = 10
  blog.page_link = "page/{num}"
end

page "/feed.xml", layout: false
set :css_dir, 'stylesheets'
set :js_dir, 'javascripts'
set :images_dir, 'images'

configure :build do
  # set :http_prefix, "/Content/images/"
end

```
Não se esqueça de adicionar a linha `gem 'nokogiri'` ao seu arquivo `blog/Gemfile`

## Configurando a página inicial

Todo conteúdo da página inicial do blog, encontra-se no arquivo `/source/index.html.erb` , 
vamos editar para mostrar os últimos 10 posts, data de criação de cada post, tags,
author e um resumo do post, seu arquivo deve ficar assim:

```erb
---
pageable: true
per_page: 10
---
<!-- 
  links de paginação que ativamos no config.rb
-->
<% if paginate && num_pages > 1 %>
  <p>Page <%= page_number %> of <%= num_pages %></p>

  <% if prev_page %>
    <p><%= link_to 'Previous page', prev_page %></p>
  <% end %>
<% end %>

<% page_articles.each_with_index do |article, i| %>
  <article>
    <!-- link para acessar o post-->
    <h2> <%= link_to article.title, article %></h2> 
      <p>
    <!-- mostra a data de criação do post-->
        <%= article.date.strftime('%e/%m/%Y') %> - 
    <!-- mostra o author post-->
        <%= article.data.author %>
      </p>
      <p>
    <!-- mostra resumo do post -->
        <%= article.summary %>
      </p>
      <p>
    <!-- mostra as tags -->
        <% article.tags.each do |tag| %>
          <a href="/tags/<%= tag.downcase %>.html">  <%= tag %></a>
        <% end %>  
      </p>
      <hr>
  </article>
<% end %>

<!-- 
  links de paginação que ativamos no config.rb
-->
<% if paginate %>
  <% if next_page %>
    <p><%= link_to 'Next page', next_page %></p>
  <% end %>
<% end %>
```

Pronto! Temos a página inicial reestruturada.

## Configurando a página do Post

Primeiro modifique a linha `blog.layout = "post"`  no arquivo `/blog/config.rb` ,
com isso estamos setando que o post deverá ter um layout diferente ao layout padrão.
Crie a pasta `source/layouts` e dentro dela o arquivo `post.erb`  com as seguintes 
configurações:

```erb
<% wrap_layout :layout do %>
  <article class="post">
    <h1><%= current_article.title %></h1>
    <p> 
      <!-- mostra o author post-->
      <%= current_article.data.author %> - 
      <!-- mostra a data de criação do post-->
      <%= current_article.date.strftime('%e/%m/%Y') %>
      <br />
      <!-- mostra as tags -->
      <% current_article.tags.each do |tag| %>
        <a href="/tags/<%= tag.downcase %>.html">  <%= tag %></a>
      <% end %>   
    </p>
    <hr>
    <p>
    <!-- renderiza o conteúdo  -->
      <%= yield %>
    </p>
  </article>
<% end %>
```

## Configurando a página

Nossa última página a configurar: "tags" ficará parecida com a "index" com a 
única diferença do apontamento no topo a qual tag estamos buscando, vamos editar 
o arquivo `source/tag.html.erb`:

```erb
---
pageable: true
per_page: 10
---
<h1>Posts com a tag: '<%= tagname %>'</h1>

<!-- 
  links de paginação que ativamos no config.rb
-->
<% if paginate && num_pages > 1 %>
  <p>Page <%= page_number %> of <%= num_pages %></p>

  <% if prev_page %>
    <p><%= link_to 'Previous page', prev_page %></p>
  <% end %>
<% end %>

<% page_articles.each_with_index do |article, i| %>
  <article>
    <!-- link para acessar o post-->
    <h2> <%= link_to article.title, article %></h2> 
      <p>
    <!-- mostra a data de criação do post-->
        <%= article.date.strftime('%e/%m/%Y') %> - 
    <!-- mostra o author post-->
        <%= article.data.author %>
      </p>
      <p>
    <!-- mostra resumo do post -->
        <%= article.summary %>
      </p>
      <p>
    <!-- mostra as tags -->
        <% article.tags.each do |tag| %>
          <a href="/tags/<%= tag.downcase %>.html">  <%= tag %></a>
        <% end %>  
      </p>
      <hr>
  </article>
<% end %>

<!-- 
  links de paginação que ativamos no config.rb
-->
<% if paginate %>
  <% if next_page %>
    <p><%= link_to 'Next page', next_page %></p>
  <% end %>
```

## Conclusão

Nesse post aprendemos como mostrar os atributos dos posts como
"author", "date", "tags" e etc,  diretamente nas views.
Aprendemos também como separar os posts por tag, que é um recurso muito usado 
para agrupar assuntos semelhantes. Qualquer configuração pode ser feita de forma
simples através do arquivo config.rb, novamente o Middleman nos permite nos 
preocuparmos somente com o conteúdo do blog e deixar toda complexidade com ele.

** Todo código gerado nesse exemplo você pode encontrar no [link](https://github.com/futrica/exemplo_blog)
