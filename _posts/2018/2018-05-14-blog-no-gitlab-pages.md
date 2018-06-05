---
layout: post
title:	"Esse blog agora está no Gitlab Pages!"
date:	2018-05-14 01:00:00
categories:
    - tips
tags:
    - git
    - gitlab
---

Rapaz, não é que esse negócio de faculdade ocupa tempo mesmo?! Pois bem, primeiro post de 2018 depois de muito, muito tempo!! \o/

Vim aqui anunciar para vocês que esse blog agora está no [Gitlab Pages \[0\]][0]!! Gitlab Pages é um projeto similar ao Github Pages que já é bastante conhecido mundo a fora. Há algumas diferenças básicas e bem interessantes, por exemplo:

- Aceitar diversos outros geradores de sites estáticos (não apenas o Jekyll);
- Ter já o pipelining do Gitlab a disposição;
- Melhor para depurar problemas!!!

Como estou usando há pouco tempo, ainda não conheço tudo que poderia daqui, mas já vi todas essas vantagens. O que eu quis dizer com "melhor para depurar problemas" é que a geração de páginas do Gitlab Pages utiliza do CI do Gitlab, portanto, temos disponíveis os logs para nos ajudar a debuggar caso algo errado aconteça, enquanto que no Github Pages você apenas recebe um e-mail informando que o processo de build falhou. Isso quando recebe :/

Mas o que me fez mudar para cá mesmo foram esses motimos:

- Free ;)
- CI
- problema--

Explico:

### Free

Bem, sabemos que o Gitlab é free, certo? Código fonte aí para fazermos modificações, utilizar em nossas comunidades de maneira gratuita, enfim, não preciso falar mais sobre isso. Portanto, queria passar a utilizar mais as coisas por aqui, mas se tornava difícil pois a adoção das pessoas é pouca, então não adianta eu querer utilizar apenas Gitlab enquanto todos códigos para contribuir estão no Github. (não falando que aqui não há nenhum projeto, obviamente!)

### CI

Outra coisa é que quero estudar mais como funciona algumas dessas práticas de buzzwords (ou será que não são?) como CI, CD, DevOps... E vi na ferramenta de integração contínua daqui do Gitlab uma boa opção para começar a botar mão nisso. :)

### problema--

Mas o **PRINCIPAL** motivo é esse aqui: **PROBLEMA--**!!

Há muito tempo atrás meu blog parou de funcionar no Github. De uma hora para outra as coisas já não funcionavam direito, css quebrado, js também... Comecei trocar e-mail com o pessoal do suporte lá em outubro de 2017. Vários e-mails trocados mas nada funcionava. Várias sugestões de como resolver, sempre levando em conta que o problema era no código do blog.

Acontece que a geração de páginas funcionava perfeitamente localmente e em alguns outros locais que testei, menos no Github. O que cheguei a ver do problema foi que o Github Pages passou a ter algum problema na interpretação da variável `baseurl` das configurações do Jekyll que não funcionava mais.

Depois de um tempo, tomei vergonha na cara e resolvi testar aqui no Gitlab. Apenas migrei o projeto e fiz algumas pequenas alterações e PRONTO, funcionando tudo certo!!

## Modificações

Para poder trazer mais informações para vocês, aqui estão as modificações que precisei fazer:

### .gitlab-ci.yml

Precisei criar o arquivo para ser utilizado pelo CI do Gitlab e gerar as páginas. Utilizei como exemplo o projeto com [jekyll \[1\]][1] aqui do próprio Gitlab Pages, para facilitar o trabalho, já que não tinha conhecimento nenhum sobre esse assunto. O conteúdo foi o seguinte:

~~~yml
image: ruby:2.3

variables:
  JEKYLL_ENV: production

before_script:
  - bundle install

test:
  stage: test
  script:
  - bundle exec jekyll build -d test
  artifacts:
    paths:
    - test
  except:
  - master

pages:
  stage: deploy
  script:
  - bundle exec jekyll build -d public
  artifacts:
    paths:
    - public
  only:
  - master
\ No newline at end of file
~~~

### Gemfile

Quando rodei o pipelining vi que deu [pau no job \[2\]][2] e não conseguiu rodar. Aqui está, por exemplo, o benefício de ter os logs podendo ser visualizados por nós, consegui perceber que o problema é que faltava um arquivo de Gemfile para definir as dependências direito:

~~~ruby
source "https://rubygems.org"
ruby RUBY_VERSION

# This will help ensure the proper Jekyll version is running.
gem "jekyll", "3.4.0"

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
\ No newline at end of file
~~~

### feed.xml

E por fim, depois que já estava com o blog rodando e funcionando, vi que algo estava com problemas: o Feed RSS.

Bem, feed rss no meu caso é algo crucial, pois não faço divulgação desse site em lugar nenhum, basicamente todos visitantes que chegam aqui é por buscadores ou já viu em algum lugar e então assinou o feed. Portanto, perder esse pessoal que assina seria bem ruim.

Fui depurar e vi que o problema estava no link do feed. Eu havia configurado a variável `permalink` no arquivo do feed para que ficasse uma url bonitinha, sem precisar da extenção do arquivo. Acontece que tava tendo problema e o Gitlab não gerava isso. A forma como testei e de fato corrigiu foi removendo essa variável e aceitando ficar com o link `feed.xml` mesmo.

Insatisfeito com essa solução, fui pesquisar para entender o real motivo disso e vi [aqui \[3\]][3] e [aqui \[4\]][4] o pessoal conversando sobre esse problema. :P

## Talvez eu tenha voltado ... :P

Bem, então fica aqui esse post rapidinho para justificar a migração do blog e convidar a todos que estavam assinados no feed continuarem, utilizando o link atual.

No mais, forte abraço a todos e vamos nessa! \o/

## Links

~~~
[0]: https://about.gitlab.com/features/pages/
[1]: https://gitlab.com/pages/jekyll/
[2]: https://gitlab.com/gildasio/gildasio.gitlab.io/-/jobs/61759056
[3]: https://gitlab.com/pages/jekyll/issues/6
[4]: https://gitlab.com/gitlab-org/gitlab-pages/issues/9
~~~

[0]: https://about.gitlab.com/features/pages/
[1]: https://gitlab.com/pages/jekyll/
[2]: https://gitlab.com/gildasio/gildasio.gitlab.io/-/jobs/61759056
[3]: https://gitlab.com/pages/jekyll/issues/6
[4]: https://gitlab.com/gitlab-org/gitlab-pages/issues/9
