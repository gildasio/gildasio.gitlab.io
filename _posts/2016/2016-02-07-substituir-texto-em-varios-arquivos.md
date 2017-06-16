---
layout: post
title:  "Dica Rápida :: Substituição de Texto em Vários Arquivos"
date:   2016-02-07 03:00:00
categories:
    - tips
tags:
    - cli lindo!
    - dicas
    - linux
    - programacao
    - sed
    - shellscript
    - terminal
---

## Enrolação

Fala pessoal! Acredito que posts como esse e [o de python \[0\]][0], que são dicas rápidas, sem dissertar muito a cerca de um assunto, pode se tornar mais comum por aqui. Espero que seja útil para vocês e para mim (como repositório para não esquecer alguns truques =]).

Bem, o que aconteceu foi o seguinte: noutro dia precisei fazer [essa \[1\]][1] alteração aqui na estrutura do blog. Isso pelo motivo de que o Github [fez uma alteração no esquema deles \[2\]][2] interpretarem o markdown. Basicamente falando, eles vão tirar o `redcarpet` (que era o interpretador padrão do GitHub Pages) passando a utilizar o `kramdown`.

O problema é que isso mexe um pouco com a sintaxe do markdown. Antes eu utilizava aquele esquema de três crases para informar um bloco que eu quisesse mostrar como pré formatado. Mas agora passou a ser três tils (~).

Menos mal que ainda estão dando suporte ao `redcarpet` e portanto vocês não viram a alteração que causava. Como sou brother, vou deixar aqui um print:

![Print da quebra de layout]({{ site.baseurl }}images/posts/2016/09.png)

Eis o impasse: atualizar todos arquivos para a nova sintaxe.

Editar arquivo por arquivo? Seria uma opção. Mas eu não estaria honrando o sistema GNU que uso :)

## Vamos lá

Resolvi isso apenas com um comando. Olha ele ai abaixo depois a explicação:

~~~
$ sed -i 's/```/~~~/g' *
~~~

Pois é! Simpls, não?! Entrei no [diretório com todos os posts \[3\]][3] e rodei o comando.

Vamos entender:

### sed

#### O que é?

~~~
> whatis sed
sed (1p)             - stream editor
~~~

Ou seja: é um editor do que é mostrado em tela, por assim dizer.

### -i

~~~
  -i[SUFFIX], --in-place[=SUFFIX]
                 edit files in place (makes backup if SUFFIX supplied)
~~~

Então indica que é para editar os arquivos de determinado lugar. Nesse caso, do nosso diretório atual.

### 's/```/~~~/g'

É o script. O coração dessa dica. Para usuário de vim, por exemplo, fica bastante familiar.

#### Estrutura

* *s* na frente representa, basicamente, o comando de substituição.
* *```* é o termo para substituir
* *~~~* é o que quero colocar no lugar
* *g* indica que é algo global


### *

É um *wildcards* (ou coringa). Nesse caso, ele indica que são todos arquivos da pasta.

## Resultado

Pronto! Olha um print da mesma página que tirei acima após rodar o comando:

![Print resolvido!]({{ site.baseurl }}images/posts/2016/10.png)

> Até mais ver, pessoal! Tomara que esse tipo de post seja de ajuda a todos :P

## Links

~~~
[0]: {{ site.url }}{{ site.baseurl }}blog/python-diferenca-operadores/
[1]: https://github.com/gjuniioor/gjuniioor.github.io/commit/141ab6bdfc50a204cfa76a2b1c804ab184620ca8
[2]: https://help.github.com/articles/updating-your-markdown-processor-to-kramdown/
[3]: https://github.com/gjuniioor/gjuniioor.github.io/tree/master/_posts
~~~

[0]: {{ site.url }}{{ site.baseurl }}blog/python-diferenca-operadores/
[1]: https://github.com/gjuniioor/gjuniioor.github.io/commit/141ab6bdfc50a204cfa76a2b1c804ab184620ca8
[2]: https://help.github.com/articles/updating-your-markdown-processor-to-kramdown/
[3]: https://github.com/gjuniioor/gjuniioor.github.io/tree/master/_posts
