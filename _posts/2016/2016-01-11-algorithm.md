---
layout: post
title:  "Filme :: Algorithm"
date:   2016-01-11 15:30:00
categories:
    - reviews
tags:
    - espionagem
    - filme
    - hacking
    - privacidade
    - seguranca
---

Algorithm (ou "Algoritmo") é um filme de 2014 que tem o tema *hacking* muito envolvido. A história é bacana. A filmagem. Trilha sonora. Todos esses aspectos são bem feitos, julgados por mim. Mas claro, vamos analisar a abordagem técnica que nele é feita. De todos os filmes que já vi sobre o tema, é o que mais gostei. A realidade nele também é bastante presente. Claro, aspectos *hollywoodianos* tem, mas por trás disso há verdades.

Nele tem passagens da [ideologia \[0\]][0] e [ética hacker \[1\]][1] [\[2\]][2] bem marcantes. As opiniões ditas também são bastante comum em pessoas desse meio:

~~~
"When I look around I don't see borders walls or locks. I see puzzles."

"Quando eu olho em volta não vejo barreiras, paredes ou fronteiras. Eu vejo desafios."
~~~

Ou, outro exemplo:

~~~
"Information should be free."

"Informação deve ser livre."
~~~

Que é um dos princípios do que é dito como **ética hacker**. São eles:

* Sharing (Compartilhamento)
* Openness (Abertura)
* Decentralization (Descentralização)
* Free access to computers (Livre acesso aos computadores)
* World Improvement (Melhoria do mundo)

Há momentos em que parece se passar em algum [hackerspace \[3\]][3] (ou makerspace):

![Cena em um possível hacker/maker space"]({{ site.baseurl }}images/posts/2016/01.jpg)

O que por se torna bem possível, já que se passa em San Francisco, lugar onde [há vários \[4\]][4] desses ambientes.

Outro ponto bastante importante são as dicas reais que são dadas. Como por exemplo, de onde fazer certos testes:

~~~
"[...] the point is, i'm not doing this from home."

"[...] o ponto é, eu não estou fazendo isso de casa."
~~~

E claro, que não podia faltar, um tempo falando sobre senhas, spams e como isso é pego no ato de uma engenharia social:

~~~
"Do you know where the weakest link in any security system is? It's you, with your shitty passwords and how you share every part of your life online [...] And your willingness to click on links that promise something you want."

"Você sabe onde o elo mais fraco em qualquer sistema de segurança está? Está em você, com suas senhas de merda e como você compartilha cada parte de sua vida online [...] E sua vontade de clicar em links que prometem algo que você quer."
~~~

> Sobre a questão do spam abordado na passagem acima, recomendo que assistam a [essa palestra \[5\]][5] cômica que alguém me enviopu recentemente:

<iframe src="https://embed-ssl.ted.com/talks/james_veitch_this_is_what_happens_when_you_reply_to_spam_email.html" frameborder="0" allowfullscreen=""></iframe>

Além dessas dicas ditas há assuntos técnicos que são abordados e explicados - claro, de maneira rápida - o que são. Por exemplo:

* Can of worms

> O termo representa algo que ao fazer vai gerar mais problemas. No filme, é utilizado uma lata com um microcomputador para derrubar/invadir/utilizar WiFi alheios. Algo como aquela [antena de pringles \[6\]][6] aquipado com um Raspberry Pi.

* Black rooms

> É dito que é um quarto, todo revestido por uma espécie de papel laminado para refletir sinais de rádio e portanto dificultar a localização. Foi utilizaro no filme quando o protagonista queria descobrir o endereço destino a que uma aplicação se comunicava mas fazer isso com o mínimo de chance de ter sua localização descoberta.

* Port knocking

> Trata-se de uma técnica de hardening em que é preciso enviar pacotes a determinadas portas (em sequência, ou não) de um servidor para que ele permita a sua conexão com uma outra porta em específico. Na obra, foi mostrado que por conta disso ele não conseguiu previamente o que desejava.

* Tor

> É uma rede utilizada para garantir o anonimato de quem o usa. Foi utilizado pelo protagonista para poder acessar o sistema de rastreamento, diminuindo o risco de ser encontrado.

E por fim, um ponto que acredito ser interessante de se tratar é o intuito das atividades de certos orgãos. Em um determinado momento, um agente recém chegado à agência de investigação mostra todo seu fôlego pelos casos, afinal, para ele se tratava de combater o terrorismo. Em contrapartida, um agente mais experiênte deu a entender que ele havia muito o que aprender ainda. Provavelmente a intenção de todo esse rastreamento está incluso nisso.

> E isso foi algo que até abordei em um outro post aqui do blog: [The Snowden Files \[7\]][7]. Que é falando minha opinião sobre um livro que em resumo: é muito bom!

Caso tenha interesse de assistir a esse filme, não precisa se preocupar em procurar muito. Ele está no Youtube e portanto, pode assistir daqui mesmo:

<iframe src="https://www.youtube.com/embed/6qpudAhYhpc" frameborder="0" allowfullscreen></iframe>

## Links

~~~
[0]: http://www.phrack.org/issues/7/3.html#article
[1]: https://en.wikipedia.org/wiki/Hacker_ethic
[2]: https://pt.wikipedia.org/wiki/Ética_hacker
[3]: http://raulhc.cc/Doc/HackerSpace
[4]: https://wiki.hackerspaces.org/San_Francisco
[5]: https://www.ted.com/talks/james_veitch_this_is_what_happens_when_you_reply_to_spam_email
[6]: http://www.binarywolf.com/249/pringles_cantenna.htm
[7]: {{ site.url }}{{ site.baseurl }}books/the-snowden-files/
~~~

[0]: http://www.phrack.org/issues/7/3.html#article
[1]: https://en.wikipedia.org/wiki/Hacker_ethic
[2]: https://pt.wikipedia.org/wiki/Ética_hacker
[3]: http://raulhc.cc/Doc/HackerSpace
[4]: https://wiki.hackerspaces.org/San_Francisco
[5]: https://www.ted.com/talks/james_veitch_this_is_what_happens_when_you_reply_to_spam_email
[6]: http://www.binarywolf.com/249/pringles_cantenna.htm
[7]: {{ site.url }}{{ site.baseurl }}books/the-snowden-files/
