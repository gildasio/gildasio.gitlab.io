---
layout: post
title:  "Habilitando autocomplete para sudo, man e etc"
date:   2015-05-17 10:29:47
categories:
    - tips
tags:
    - linux
    - terminal
---

Olá, pessoal! Esse post na verdade é uma repostagem de uma dica minha postada no [Viva o Linux](http://vivaolinux.com.br/~gjuniioor "Viva o Linux").

É algo básico, mas que é estupendamente irritante quando se tem o problema. Eu sou daqueles que usam - *ou fingem que usam* - CLI para tudo, ou quase.

Antes de mostrar o pulo do gato - que é bem simples na verdade - vou deixar dois exemplos de situações que vocês podem ver a utilidade dessa dica.

**Exemplo 01**: Você, de forma alguma, usa o usuário root para fazer algo. Sempre que precisa elevar privilégio a esse nível para algum procedimento, faz uso do sudo para isso (*e está corretíssimo!*). Mas, sempre que utiliza o *sudo*, tem de digitar o comando, caractere por caractere, e isso é um pouco chato.

**Exemplo 02**: Então, dia lindo de sol, você está trabalhando em algo e precisa verificar determinada opção em alguns comandos para ver se resolvem. Vai, claro, utilizar o *man* para ter todos os detalhes e tudo mais. O problema é que sempre que vai usar o man, nunca tem como adiantar a digitação pressionando Tab.
<!--more-->
**Pois é, gafanhoto, vamos resolver isso...**

O que teremos de fazer é adicionar uma determinada regra ao shell para que ele entenda que deve completar os parâmetros dos programas determinados, com outros comandos. E isso é feito com um simples comando, veja para o *sudo* como ficaria:

~~~
$ complete -cf sudo
~~~

E para o *man*:

~~~
$ complete -cf man
~~~

Como são simples comandos, podemos adicioná-los aos arquivos que são executados quando abrimos uma janela de terminal.

Para nosso usuário atual apenas:

~~~
$ vim ~/.bashrc
~~~

E para qualquer usuário do sistema:

~~~
# vim /etc/bash.bashrc
~~~

*P.S.*: Essa dica não é válida apenas para o *sudo* e *man*, abra sua mente e pense em novas perspectivas de uso também, como por exemplo para o *whatis*, *whereis* e demais! :)

Bem, é isso... Dica simples mas bem útil a meu ver. Obrigado pela leitura e até a próxima.

*Artigo previamente publicado [aqui](http://www.vivaolinux.com.br/dica/Habilitando-autocomplete-para-o-sudo-e-man/ "Publicado no Viva o Linux")*

**UPDATE!!**

Após postado no [Viva o Linux](http://www.vivaolinux.com.br/dica/Habilitando-autocomplete-para-o-sudo-e-man/ "Dica no Viva o Linux") a dica recebeu contribuições de alguns usuários de lá. E aqui, eu posto os comentários que foram interessantes também!

Pelos usuário [eldermarco](http://www.vivaolinux.com.br/~eldermarco "Perfil no Viva o Linux") e [lcavalheiro](http://www.vivaolinux.com.br/~eldermarco "Prefil no Viva o Linux"): Ambos citaram o uso do pacote **bash-completion** alegando que ele resolve esse problema de autocompletar para vários comandos. Eu testei esse programa e sim, ele compre o esperado! Autocompleta com maestria a maioria dos comandos e alguns até melhor, de certa forma, que partindo da análise do post!

Mas para quem prefere fazer as coisas na mão, bem, o programa é opcional. ^-^