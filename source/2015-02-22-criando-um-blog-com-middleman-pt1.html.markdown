---
title: Criando um blog com middleman
date: 2015-02-22 00:12 BRT
tags: blog, middleman
author: Futrica
---

Neste post vamos mostrar como é rápido e fácil criar e manter um blog usando a ferramenta Middleman, esse tópico será divido em 3 posts: Instalação e configuração do Middleman; Configuração e Desenvolvimento; Deploy da aplicação usando Heroku.

## Primeiro ... o que é *Middleman?*

*"Middleman is a static site generator using all the shortcuts and tools in modern web development."*

[Middleman](https://middlemanapp.com/) é uma ferramenta gratuita, criada pela [Thoughtbot](https://thoughtbot.com/), para geração de páginas estáticas.
O framework se encarrega de fazer todo o trabalho como: estrutura de diretórios, criação das rotas, as views e etc. e você só se preocupar com o conteúdo.

## Instalando o Middleman

Middleman é distribuído através de uma [RubyGem](https://rubygems.org/) ou Gem, que nada mais é que uma biblioteca de arquivos reutilizáveis em Ruby.
Para instalação é necessário  que tenha instalado em sua máquina a linguagem de programação Ruby e o Framework gerenciador RubyGems.
Acesse: [https://www.ruby-lang.org/en/downloads/](https://www.ruby-lang.org/en/downloads/) para instruções de como instalar Ruby.

Um vez com todos os requisitos instalados, basta abrir um terminal e digitar o seguinte comando:

`$ gem install middleman`

Pronto! Basta esse simples comando para poder usar o Middleman.

Agora só ir ao terminal novamente e digitar:

`$ middleman init seu_site`
Com isso toda estrutura do site é criada automaticamente … Mas calma aí vamos criar um blog … 

## Criando nosso Blog
Middleman ainda conta com uma gem específica para criação de blog. Para instalar:

`$ gem install middleman-blog`

Com a instalação pronta basta rodar o comando para criar toda estrutura do blog, *middleman* + comando *init* + *nome do seu blog* + *--template escolhido* . Vamos ao comando

`$ middleman init blog --template=blog`

Vamos entender o que foi gerado:


`create  blog/.gitignore` = *arquivo que o github deve ignorar* <br />
`create  blog/config.rb` = *arquivo para configuração da página*<br />
`create  blog/source` = *diretório com o "esqueleto" do site*<br />
`create  blog/source/2012-01-01-example-article.html.markdown` = *exemplo de post* <br />
`create  blog/source/calendar.html.erb` = *comportamentos de datas*<br />
`create  blog/source/feed.xml.builder` = *arquivo para configuração*<br />
`create  blog/source/index.html.erb` = *página inicial do site*<br />
`create  blog/source/layout.erb` = *arquivo de layout*<br />
`create  blog/source/tag.html.erb` = *página de tags*<br />
`create  blog/source/stylesheets`  = *pasta para armazenar os arquivos css*<br />
`create  blog/source/javascripts` = *pasta para armazenar os arquivos css*<br />
`create  blog/source/images` = *diretório para armazenar imagens* <br />



Com isso já é possível rodar seu novo site, vá ao terminal e digite:

`$ middleman server`


> se por acaso tiver um erro parecido com o abaixo:
>
> */.rvm/gems/ruby-2.2.0/gems/execjs-2.3.0/lib/execjs/runtimes.rb:45:in `autodetect': Could not find a JavaScript runtime. See https://github.com/sstephenson/execjs for a list of available runtimes. (ExecJS::RuntimeUnavailable)*
>
> Não se preocupe, a solução é simples, basta adicionar ao arquivo Gemfile a gem therubyracer, com a seguinte linha abaixo: <br />
> `gem ‘therubyracer’`
> e rodar o comando <br />
> `$ bundle` <br />
> ou instalar [nodeJS](http://nodejs.org/) <br />
> Esse erro se dá pela falta de um compilador para os assets.

Analisando a saída do comando: <br />
`== The Middleman is loading` <br />
`== The Middleman is standing watch at http://0.0.0.0:4567` <br />
`== Inspect your site configuration at http://0.0.0.0:4567/__middleman/`


Podemos perceber que o site já está rodando, basta acessar o navegador em ‘localhost’ na porta indicada 4567, http://localhost:4567

 ![alt text](/images/blog.png "blog no ar!") 

Toda a estrutura pronta com um só comando, já podemos navegar no posts, alinhar os posts por data ou por tags.

Agora, vamos criar um novo post, basta digitar no termina a seguinte estrutura “ middleman + article + nome-do-post (separo por traço):

`$ middleman article exemplo-post`

Veja que foi criado um arquivo novo: “data da criação” + “nome do post”:

`create  source/2015-02-23-exemplo-post.html.markdown`

Vamos dar uma olhada nesse arquivo criado, temos o cabeçário:

--- <br />
title: exemplo-post <br />
date: 2015-02-23 13:19 UTC <br />
tags: <br />
--- 

Sendo que: <br />

--- <br />
title = nome do post <br />
date =  data da criação do post
tags = palavras para categorizar o assunto(separados por virgula) , exemplo: (ruby, rails).
podemos ainda adicionar a informação do autor do post: <br />
author: “Nome do autor” <br />
---

** aqui vai todo o conteúdo do post **


O arquivo padrão gerado tem a extensão “.markdown” que é uma linguagem de marcação dinâmica e simples de usar, para mais informações: [Documentação Markdown](https://help.github.com/articles/github-flavored-markdown/)

## Conclusão 

Middleman é um framework que facilita bastante a criação de páginas simples e performáticas, abstraindo toda a complexidade do código, nos fazendo focar no que realmente é importante: o conteúdo.

** todo código gerado nesse exemplo você pode encontrar no [link](https://github.com/futrica/exemplo_blog)
