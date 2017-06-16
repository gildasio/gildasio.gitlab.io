---
layout: post
title:  "Dica Rápida :: Redimensionar Imagens via Linha de Comando"
date:   2016-02-17 02:00:00
categories:
    - tips
tags:
    - cli lindo!
    - dicas
    - imagemagick
    - shellscript
    - terminal
---

Por agora, recentemente mesmo, colocamos o [blog do PHPBA \[0\]][0] no ar!! Todo o código está no [repositório no Github \[1\]][1]. Feito utilizando o [Jekyll \[2\]][2], assim como esse meu blog aqui. =] 

A questão é que o [tema \[3\]][3] que utilizamos lá tem umas configurações para ser compatível com vários dispotivos e por isso precisou de imagens de várias dimensões. Em um [PR \[4\]][4] que eu fiz, [modifiquei todas as imagens \[5\]][5] padrão que tinha para serem o mascote do PHPBA nessas dimensões.

Agora imagine o trabalhão que não seria ter de utilizar um serviço web que tem de subir uma imagem, selecionar o tamanho, esperar converter e por fim baixar a imagem, renomeando tudo conforme padrão ... Pois bem, mas, novamente falando:

> [**Seria uma opção. Mas eu não estaria honrando o sistema GNU que uso :)** \[6\]][6]

Resolvi com um simples laço `for` e com o imagemagick! Esse conjunto de programas tem um chamado `mogrify` que além de várias funções, tem a de redimensionar uma imagem. Vejamos:

~~~
$ mogrify -resize 190 elephpant.jpg
~~~

Esse foi o comando utilizado para redimensionar da forma que estava para 190x190. No caso, a imagem utilizada já estava na forma de um quadrado, pois esse comando vai calcular a outra dimensão para que a imagem não fique deformada. Aqui segue outros truques:


* Converte a imagem *elephpant.jpg* para o formato PNG salvando em *elephpant.png*.

~~~
$ mogrify -format png elephpant.jpg elephpant.png
~~~

* Rotaciona em 90° para a direita a imagem *elephpant_normal.jpg*, salvando em *elephpant_deitado.jpg*

~~~
$ convert -rotate 90 elephpant_normal.jpg elephpant_deitado.jpg
~~~

Bem, agora sim, acredito que segui o ideal de "[Dicas rápidas \[7\]][7]" haha ... Até mais ver!!

## Links

~~~
[0]: http://phpba.com.br
[1]: https://github.com/phpba/phpba.github.io
[2]: http://jekyllrb.com/
[3]: https://github.com/bencentra/centrarium
[4]: https://github.com/phpba/phpba.github.io/pull/7
[5]: https://github.com/phpba/phpba.github.io/commit/59faf1a02a6a22985baa385018444955307b64f3
[6]: {{ site.url }}{{ site.baseurl }}blog/substituir-texto-em-varios-arquivos/
[7]: {{ site.url }}{{ site.baseurl }}category/#dicas
~~~

[0]: http://phpba.com.br
[1]: https://github.com/phpba/phpba.github.io
[2]: http://jekyllrb.com/
[3]: https://github.com/bencentra/centrarium
[4]: https://github.com/phpba/phpba.github.io/pull/7
[5]: https://github.com/phpba/phpba.github.io/commit/59faf1a02a6a22985baa385018444955307b64f3
[6]: {{ site.url }}{{ site.baseurl }}blog/substituir-texto-em-varios-arquivos/
[7]: {{ site.url }}{{ site.baseurl }}category/#dicas
