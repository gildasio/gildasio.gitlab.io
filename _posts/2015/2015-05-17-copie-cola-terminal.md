---
layout: post
title:  "Copie/Cole conteúdo do terminal para o X e vice-versa"
date:   2015-05-17 10:29:46
categories:
    - tips
tags:
    - linux
    - terminal
---

Fala gente! Esse post é bem útil para aqueles que, como eu, usam bastante o terminal mas em algum momento precisam copiar alguma coisa para colar em outro lugar através do X.

Para isso vamos precisar de um programa, mas trago dois como opções. Eu tenho um preferido - *uma dica: a pronúncia parece com um software da MS* - mas fica para você escolher o seu. ;)

Os programas são<!--more-->: *xsel* e *xclip*. Ambos bem conceituados e provavelmente estão nos repositórios de sua distribuição (*a menos que você use Slackware e afins, mas eles estão lá no SlackBuilds também* ^-^).

## Instalação

*P.S.*: O procedimento de instalação não vou mostrar aqui, afinal, pressuponho que quem busca uma dica como essa saiba instalar um programa em sua distro, usando APT, aptitude, pacman, yum, SlackBuilds ou afins... Caso não saiba, tutoriais é o que não falta por ai. **Sabendo disso, vamos seguindo.**

## Definindo: *Selections*

Tenha em mente que esses programas trabalham com o conceito de *selections*.
O que seria isso?

Bem, é a partir daí que eles direcionam a atuação para a selection *primária*, *secundária*, *clipboard*... A *clipboard* é a tal "*área de transferência*", a que é alterada pelo "*Ctrl + c/v*", pelo X. A primária (*primary*) e a secundária (*secondary*) são variáveis que o próprio programa cira e utiliza.

Sendo que a que nos interessa mesmo, nesse artigo (e no dia a dia), é a *clipboard*.

No *xsel*, para selecionarmos o *clipboard* como a selection a usar é da seguinte forma:

~~~
$ xsel -b
$ xsel --clipboard
~~~

Ou um ou outro comando. Ambos fazem o mesmo efeito. Já no *xclip* é:

~~~
$ xclip -selection clipboard
~~~

Sabendo disso, vamos usar sempre a seleção agora para poder fazer as alterações direto na nossa área de transferência.

## Ctrl + V

Para a função de "*Ctrl + v*", que seria a de exibir o conteúdo da área de transferência para a tela, ou algum arquivo, vejamos como fazer...

É bem simples. Em ambos os programas fazemos da mesma forma:

~~~
$ xsel -o
$ xclip -o
~~~

Mas saiba também que se o *xsel* não for acompanhado de nenhuma opção, o padrão é ele exibir o conteúdo. Logo, o comando acima equivale a:

~~~
$ xsel
~~~

Esses comandos vão exibir o conteúdo do *clipboard* na tela. Para passar para um arquivo, como valor de um programa, e outras funções afins, basta direcionar seu fluxo. Veja um exemplo para salvar no arquivo de nome *cv.txt* no diretório */tmp*:

~~~
$ xsel > /tmp/cv.txt
$ xclip -o > /tmp/cv.txt
~~~

## Ctrl + C

Já vimos como fazer a colagem do que temos na área de transferência, mas antes de colar, temos de copiar, certo?!

Então vamos lá... No início do texto eu disse que o de minha preferência é o *xsel* e aqui ele já começa a se destacar. Vejamos...

No *xclip* podemos fazer a cópia da seguinte maneira:

~~~
$ xclip -selection clipboard /tmp/cv.txt
~~~

Utilizando o mesmo arquivo que salvamos anteriormente, só para exemplo.

E no *xsel*, podemos fazer isso de duas maneiras:

~~~
$ xsel -b < /tmp/cv.txt
$ xsel -b -i < /tmp/cv.txt
~~~

Ambos os comandos fazem o mesmo resultado. Mas agora que vem um pequeno diferencial do *xsel*: com ele, posso acrescentar (não substituir, acrescentar mesmo!) dados ao clipboard.

Para isso, posso utilizar de um parâmetro que dispomos:

~~~
$ xsel -b -a < /tmp/cv.txt
~~~

Faça a operação de *Ctrl + v* agora para verificar se não está com o conteúdo diferente! ;)

### MAIS UMAS BREVES VANTAGENS DO XSEL

Aqui vou justificar um pouco minha preferência pelo *xsel*.

#### Limpando selection

Uma opção que acho interessante dele é eu poder limpar a selection que eu quiser. Basta usar o comando:

~~~
$ xsel -c -b
~~~

#### Trocando conteúdo da primary com a secondary

Isso mesmo, para quem usa também a seleção primária e secundária dada como opções pelo programa pode ter a comodidade de trocar os seus valores usando apenas um parâmetro:

~~~
$ xsel -x
~~~

Claro que isso podemos fazer com o *xclip*, basta brincar um pouco com mais comandos nativos, mas dessa forma mostrada é bem mais simples, convenhamos! :D

#### Gerando log

Pois é! Para aqueles apaixonados (*a.k.a. psicóticos*) que gostam de saber de qualquer coisa que dê errado no computador, pode usar a opção de gerar log caso apresente algum erro na execução do procedimento.

~~~
$ xsel -l
~~~

O padrão do endereço do arquivo é *~/.xsel.log*.

*P.S.*: Artigo previamente publicado [aqui](http://www.vivaolinux.com.br/artigo/CopieCole-conteudo-do-terminal-para-o-X-e-vice-versa/ "Artigo no Viva o Linux").

## Update!!

Após postado no [Viva o Linux](http://www.vivaolinux.com.br/artigo/CopieCole-conteudo-do-terminal-para-o-X-e-vice-versa/ "Artigo no Viva o Linux") alguns usuários contribuiram com comentários, mostrando outras formas de se fazer e como eles preferiam. Segue as contribuições...

[spylinux](http://www.vivaolinux.com.br/~spylinux "Usuário no Viva o Linux"): Eu costumo usar apenas o buffer do sistema, com o mouse seleciono o texto (não precisa usar Ctrl C, apenas selecionar com o mouse) e colo via buffer usando o botão do meio do mouse(ou no notebook com o touchpad, uso 2 ou 3 dedos no touch para emular o botão do meio) e assim colo o texto selecionado, sem precisar usar Ctrl + C e Ctrl + V.

[lcavalheiro](http://www.vivaolinux.com.br/~lcavalheiro "Usuário no Viva o Linux"): Outra forma de copiar do terminal pro X e vice-versa: para copiar do X use C, mas para colar no terminal use V. Da mesma forma, para copiar do terminal use C e para colar no X use V. Lembrando que o o C ou V funcionam mesmo no caso de computadores nos quais o X não esteja rodando e que possuem o mouse habilitado para trabalhar no terminal puro (ex., instalação padrão do Slackware).

A forma mostrada pelo *lcavalheiro* eu também uso bastante e facilita muito, apenas usando uma tecla a mais nos comandos. Já pelo *spylinux* eu conhecia, mas uso pouco ou quase nunca. :)