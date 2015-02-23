---
title: Criando um blog com middleman
date: 2015-02-22 00:12 BRT
tags: blog, middleman
author: Futrica
---

Neste post vamos mostrar como é rápido e fácil criar e manter um blog usando a ferramenta Middleman, esse tópico será divido em 4 posts: Instalação e configuração do Middleman; Desenvolvimento e Estilização, Deploy da aplicação usando Heroku e Mantendo e atualizando o blog através de Pull Requests do github.

## Primeiro ... o que é *Middleman?*

*"Middleman is a static site generator using all the shortcuts and tools in modern web development."*

[Middleman](https://middlemanapp.com/) é uma ferramenta gratuita e open source, criada para facilitar o desenvolvimento de sites estáticos, *como este blog*.

O framework se encarrega de fazer todo o trabalho como: estrutura de diretórios, criação das rotas, views e etc.

Você só vai se preocupar com o conteúdo e a estilização.

## Instalando o Middleman

Middleman é distribuído através de uma [RubyGem](https://rubygems.org/) ou Gem, que nada mais é do que a forma que o Ruby lida com bibliotecas reutilizáveis..

Para sua instalação é necessário que você tenha o Ruby instalado e configurado, para isso recomendamos o [RVM](https://rvm.io/rvm/install).

Após a instalação das dependências, instalamos o middleman através do seguinte comando:

```bash
$ gem install middleman
```

Pronto! Agora só ir ao terminal novamente e digitar:

```bash
$ middleman init nome_do_site
```

Com isso toda estrutura do site é criada automaticamente … Mas calma aí vamos criar um blog … 

## Criando nosso Blog
Middleman ainda conta com uma gem específica para criação de blog. Para instalar:

```bash
$ gem install middleman-blog
```

Com a instalação pronta, basta rodar o comando para criar toda estrutura do blog:

```bash
$ middleman init nome_do_blog --template=blog
```

Vamos entender o que foi gerado:

```bash
create  blog/.gitignore #arquivo que determina os arquivos que o git deve ignorar
create  blog/config.rb #arquivo de configuração do blog
create  blog/source #diretório com o "esqueleto" do site
create  blog/source/2012-01-01-example-article.html.markdown #exemplo de post
create  blog/source/calendar.html.erb #comportamentos de datas
create  blog/source/feed.xml.builder #arquivo para criação do feed
create  blog/source/index.html.erb #página inicial do site
create  blog/source/layout.erb #layout base do site
create  blog/source/tag.html.erb #página de tags
create  blog/source/stylesheets #diretório com os estilos
create  blog/source/javascripts #diretório com os scripts
create  blog/source/images #diretório para armazenar imagens
```


Agora podemos inicializar o middleman:

```bash 
$ middleman server
```


> se por acaso tiver um erro parecido com o abaixo:
>
> */.rvm/gems/ruby-2.2.0/gems/execjs-2.3.0/lib/execjs/runtimes.rb:45:in `autodetect': Could not find a JavaScript runtime. See https://github.com/sstephenson/execjs for a list of available runtimes. (ExecJS::RuntimeUnavailable)*
>
> Não se preocupe, a solução é simples, basta adicionar ao arquivo Gemfile a gem therubyracer, com a seguinte linha:
>
> `gem ‘therubyracer’`<br />
> e rodar o comando<br />
> `$ bundle`<br />
> ou instalar [nodeJS](http://nodejs.org/) <br />
> Esse erro se dá pela falta de um compilador para os assets.

Analisando a saída do comando:

```bash
== The Middleman is loading
== The Middleman is standing watch at http://0.0.0.0:4567`
== Inspect your site configuration at http://0.0.0.0:4567/__middleman/
```

Podemos perceber que o site já está rodando, basta acessar o navegador em ‘localhost’ na porta indicada 4567, [http://localhost:4567](http://localhost:4567)

 ![alt text](/images/blog.png "blog no ar!") 

Toda a estrutura pronta com um só comando, já podemos navegar no posts, alinhar os posts por data ou por tags.

Agora, vamos criar um novo post, basta digitar no termina a seguinte estrutura "middleman + article + nome-do-post":

```bash 
$ middleman article exemplo-post
```

Veja que foi criado um arquivo novo: "data da criação" + "nome do post":

```bash 
create  source/2015-02-23-exemplo-post.html.markdown
```

Vamos dar uma olhada nesse arquivo criado, temos o cabeçalho do post:


```markdown
---
title: exemplo-post
date: 2015-02-23 13:19 UTC
tags: exemplos
--- 

Conteúdo do Post
```

Sendo que:

```markdown
---
title = nome do post
date =  data da criação do post
tags = palavras para categorizar o assunto(separados por virgula) , exemplo: (ruby, rails).
podemos ainda adicionar a informação do autor do post:
author: "Nome do autor"
#linha em branco
Conteúdo do Post
---
```

O arquivo padrão gerado tem a extensão ".markdown" que é uma linguagem de marcação dinâmica e simples de usar, para mais informações: [Documentação Markdown](http://daringfireball.net/projects/markdown/syntax)

## Conclusão 

Middleman é um framework que facilita bastante a criação de páginas simples e performáticas, abstraindo toda a complexidade do código, nos fazendo focar no que realmente é importante: o conteúdo.

** Todo código gerado nesse exemplo você pode encontrar no [link](https://github.com/futrica/exemplo_blog)
