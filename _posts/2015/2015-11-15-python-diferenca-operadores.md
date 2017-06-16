---
layout: post
title:  "Dica Rápida :: Python - Diferença entre == e is"
date:   2015-11-15 22:25:00
categories:
    - tips
tags:
    - programacao
    - python
---

Olá, galera, tudo tranquilo?

Estava conversando com um amigo que está estudando python e tudo mais, e então ele veio com a seguinte dúvida:

> Qual a diferença entre == e is no python?

> OBS: Recomendo para quem começar a ler esse post que vá até o final. Há coisas que só terão correto sentido quando complementadas. Recomendo fortemente também que leia os comentários! Há uma boa discussão a respeito disso por lá! Thanks!

Para quem não sabe, no python tem o operador *is* que "tem a mesma função" do *==*. Veja:

~~~python
>>> x = 10
>>> y = 10
>>> x == y
True
>>> x is y
True
~~~

Mas...

~~~python
>>> x = 1000
>>> y = 1000
>>> x == y
True
>>> x is y
False
~~~

Viu só? Pois bem, o que que acontece então??

O python tem um mecanismo interessante nesse ponto... Quando se tratam de *coisas pequenas* ele utiliza de ponteiros para apontar outros rótulos para um mesmo endereço de memória. Quando o que é armazenado na variável já começa a crescer, fica maior e tal, ele já não usa disso, para não pesar, mas sim de outro endereço.

Seria um cache que ele faz de alguns tipos de objetos, entre eles estão int e string, por exemplo. Float e dicionário já não são assim.

Para ter uma ideia melhor disso, vamos ver os endereços que as variáveis ocupam e o resultado da comparação:

~~~python
>>> x = 10
>>> y = 10
>>> hex(id(x))
'0x98a1844'
>>> hex(id(y))
'0x98a1844'
>>> x == y
True
>>> x is y
True
~~~

Perceba que ele pega o mesmo endereço ... Agora, se colocarmos valores maiores:

~~~python
>>> x = 1000
>>> y = 1000
>>> hex(id(x))
'0x98e5520'
>>> hex(id(y))
'0x98e5508'
>>> x == y
True
>>> x is y
False
~~~

Ou seja, o *is* (como a tradução mostra) vai verificar se algo é aquilo a que a comparação está se referindo, ou seja, se são a mesma coisa. Já o *==* vai analisar se são iguais, assim como o esperado.

Mais algumas demonstrações:

* Float:

~~~python
>>> x = 1.0
>>> y = 1.0
>>> x == y
True
>>> x is y
False
~~~

* Dict:

~~~python
>>> x = [1]
>>> y = [1]
>>> x == y
True
>>> x is y
False
~~~

> Não há motivo para me aprofundar tanto aqui, é apenas uma dica rápida. Espero que resolva os problemas de dúvidas de quem necessitar ... Tem mais algum caso como esse? Quer tirar alguma dúvida do tipo? Comenta ai ou entra em contato (olha no topo da página).

Vlw pessoal, até mais ver!!
