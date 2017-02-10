---
layout: post
title: Primeiro post, pra variar...
categories:
- blog
---

Como todo blog começa, este é o primeiro post.
Escolhi fazer o meu blog usando [Jekyll](https://jekyllrb.com/), hospedado no 
[Github Pages](https://pages.github.com/),
para não precisar pagar um host para uma coisa pequena e particular.

Pra ajudar, aqui vão algumas coisas técnicas sobre a instalação do Jekyll no 
[Cloud9](http://c9.io) que eu gostaria de lembrar depois.

Primeiro, estou configurando todo o ambiente para gerar este site no c9 (vou chamar
o Cloud9 desta forma para facilitar), por dois motivos:

1. O [meu notebook](https://www.asus.com/br/2-in-1-PCs/ASUS_Transformer_Book_T100TA/) 
só tem 2Gb de RAM. Então rodar uma máquina virtual com Linux para usar o Ruby não 
é uma tarefa fácil. VirtualBox + Chrome + Sublime 
dá pra usar, mas fica no limite do aceitável.
2. Preguiça de ficar configurando o mesmo ambiente em vários computadores.
Não tenho mais vontade de ficar instalando tudo em várias máquinas. 

Desta forma, fiz a configuração de tudo o que precisava para gerar este blog numa
workspace do c9.

# Configuração do c9
Achei que ia ser bem simples, mas demorei para conseguir colocar tudo em ordem para
fazer pelo menos este post.

Eu já tinha aprendido algumas manhas para as configurações básicas do ambiente:
{% highlight shell %}
$ rvm get head
$ rvm upgrade 2.3.0 2.4.0
$ rvm use 2.4.0 --default
{% endhighlight %}

E assim atualizei o *rvm* e instalei o Ruby mais recente.

Procurei um [tema legal](https://drjekyllthemes.github.io/) e achei esse 
[lagom](https://github.com/swanson/lagom).

Clonei o repositório num remote diferente e comecei a seguir o README. 
{% highlight shell %}
$ gem install bundler
$ bundle install
{% endhighlight %}

E deu erro na instalação da gem *"json"*.

Procurei no Google e achei uma [issue](https://github.com/github/pages-gem/issues/376)
falando de incompatibilidade do *"json"* na versão `1.8.1` com o Ruby `2.4.0`.

Então lá vou eu tentar usar outro Ruby:
{% highlight shell %}
$ rvm install 2.3.3
$ gem install bundler
$ bundle install
{% endhighlight %}

E adivinha? Mesmo erro, claro!

Continuando as buscas no Google, algum lugar tinha falando pra dar um `bundle update`
{% highlight shell %}
$ bundle update
{% endhighlight %}
Não é que foi? E assim terminou a instalação das gems.

Vamos então testar o serviço:
{% highlight shell %}
$ jekyll serve
{% endhighlight %}
Pra variar, erro. Faltou uma gem *"pygments.rb"*, que eu adicionei no `Gemfile` e instalei.

Mais algumas dificuldades para criar um Runner no c9 para no projeto. Nesse caso era
o arquivo `.ruby-version` que estava configurado na versão `2.1.5` e assim não 
carregava o Ruby certo para rodar o Jekyll.

Só para constar, o comando para colocar no runner é `jekyll serve --host $IP --port $PORT`


E assim, aprendendo um pouco de Markdown, vou terminando este post para referência futura.

Acredito que farei mais alguns posts neste blog relatando minhas novas experiências
na criação de um sistema para a igreja que frequento.

Boa noite e até mais.

* PS: Depois que fiz a primeira publicação, o Github Pages me mandou um e-mail 
pedindo para alterar a configuração do *highlighter* para *rouge* porque eles não
suportam o *pygments*.