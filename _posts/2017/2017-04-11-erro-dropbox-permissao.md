---
layout: post
title:	"Não foi possível iniciar o Dropbox [possível erro de permissão]"
date:	2017-04-11 03:00:00
categories:
    - tips
tags:
    - dropbox
    - error
    - linux
---

<div style="text-align: center;">
    <img src="{{ site.baseurl }}images/posts/2017/03.png" style="width:50%;" />
</div>

Bem, esse erro aconteceu comigo um tempão atrás. Fucei muito por ai na internet e nada de achar uma solução. Todos os posts relacionados a isso que encontrava era sempre, de fato, problemas com permissões, mas no meu caso não tinha nada disso. Verificava sempre os logs, mas nada.

Depois de muito tempo, meio que desisti de usar Dropbox, continuei com outras soluções. Um tempo depois, após formatar meu notebook, instalei DB por curiosidade e funcionou, fiquei por mais um tempo, até vir esse problema novamente. Mas dessa vez, não descansei até solucionar.

Parei para refazer meus passos e analisar cada consequência até que cheguei a perceber que o problema não tem nada a ver com permissões, mas sim com espaço de armazenamento. Aí, shablau! Agora, é só [redimensionar a partição \[0\]][0] e pronto! :)

## Links

~~~
[0]: {{ site.url }}{{ site.baseurl }}blog/redimensionar-particoes-lvm/
~~~

[0]: {{ site.baseurl }}blog/redimensionar-particoes-lvm/
