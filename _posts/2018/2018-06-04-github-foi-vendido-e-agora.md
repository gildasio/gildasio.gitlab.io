---
layout: post
title:	"Github foi vendido para Microsoft, E AGORA??"
date:	2018-06-04 01:00:00
categories:
    - posts
tags:
    - git
    - gitlab
    - github
---

Oi, pessoal!! Vamos falar de algo que está sendo bastante comentado e noticiado aí pelo mundo? Bora sim, sinhô!

Pois bem, eu gosto de abordar esses fenômenos que acontecem - como é o caso dessa notícia - a partir de outras perspectivas, como também fiz no caso do [WhatsApp \[0\]][0] quando foi bloqueado no Brasil. Então, aqui vou dar minha opinião sobre o fato e os pensamentos que me surgiram sobre isso.

* toc
{:toc}

## Contextualizando

Hoje saiu a notícia de que o Github havia sido vendido para a Microsoft. Podemos ver que não é rumor ou, algo muito falado hoje, _fake news_, pois no próprio [blog do Github \[1\]][1] e da [Microsoft \[2\]][2].

Então, pelo menos na área de tecnologia foi um alvoroço só. Quase todos os grupos de WhatsApp e Telegram sobre tecnologia que participo falaram, nem que fosse um pouco, sobre isso ao decorrer do dia, havendo, inclusive, aqueles que viraram pauta principal.

Muitas pessoas reclamando, achando ruim essa venda, como diz em um [texto curto e bacana o Shane Dowling \[3\]][3]. Outras abordagens para essa mesma questão foram feitas, como exemplo, posso levantar o [texto do Gitlab \[4\]][4] parabenizando o Github pelo feito e por toda a mudança que ele proporcionou no mundo do desenvolvimento de software, principalmente.

E claro, os memes, como não poderia faltar:

![Meme01]({{ site.baseurl }}images/posts/2018/01.jpeg)
![Meme01]({{ site.baseurl }}images/posts/2018/02.jpg)
![Meme01]({{ site.baseurl }}images/posts/2018/03.jpg)

## O que fazer?

Bom, há quem veja isso como sendo o fim do Github, há quem veja como um novo recomeço e também aqueles que acham que não vai mudar nada. Eu sou daqueles que preferem esperar um pouco para ver no que vai dar, mas parafraseando o Shane (que citei acima), espero não precisar logar com uma conta Outlook no Github daqui para frente.

Ao menos eu, que já estava migrando para o Gitlab vide [esse post \[5\]][5] que fiz um tempo atrás, continuar indo para o Gitlab é a rota default melhor até então. MUITAS outras pessoas estão fazendo isso hoje mesmo. Chega a performance daqui caiu um pouco. Uma importação de repositório, que já havia feito outras vezes, do Github para o Gitlab que durava cerca de alguns minutos já passou de uma hora e não concluiu ainda. Inclusive, de maneira empírica, apenas, notei que o meu feed de atualizações do Github está com uma movimentação menor que o normal, mas enfim, podem ser apenas coincidências.

Pois bem, se você pensa em migrar para o Gitlab (já vi comentários por aí de que essa é a chance do Gitlab crescer como nunca), nesse post vou falar um pouco sobre esse processo e também de umas features do Gitlab que acho fodas!

## Gitlab

Hoje em dia tenho muito mais experiência de projetos com o Github que com o Gitlab. Aqui já utilizei algumas features interessantes do sistema, mas não sou um conhecedor nato.

### Como migrar

Bem, primeiro, [faça sua conta \[6\]][6], obviamente. Aqui as ideias principais, e que acho muito boas que tinham no Github, também existem, como por exemplo:

* Issues
* Pull Request, ou melhor, Merge Request
* Wiki
* Fork
* Star
* ...

Portanto, the features você não sofrerá!

O Gitlab tem uma feature para você importar repositórios do Github. Isso inclui trazer todos os dados sobre ele, não só o código mas coisas como issues e pull requests também. Isso é muito massa principalmente pela importância dessas informações, né?! É!

Para isso, basta ir no menu superior na parte direita, no sinal +, e ir em New Project. Na tela dividida em abas você terá a opção de importar o projeto, e então seleciona Github. Basta seguir o que é informado na tela que você terá a possibilidade de listar TODOS seus repositórios no Github e importar um a um ou todos de vez.

Coloquei ali acima **TODOS** em maiúsculo pois achei isso bem interessante: se eu tiver como colaborador em um projeto, o Gitlab vai colocar o repositório nessa lista, permitindo com que eu importe ele facilmente.

Entretanto, é bom ter cuidado com isso, pois vai que você faça parte de algumas organizações que tem váaaaarios projetos... colocar para importar todos, imagino, não deve ser o desejado.

Agora um ponto que achei interessante também sobre essa feature do Gitlab é que ela trabalha com a ideia de falha segura. Isso seria, basicamente, você pensar como lidar em um processo de falha. O quesito que levanto é que para todo repositório que você for importar do Github dessa forma o Gitlab vai salvá-lo como repositório privado. Ou seja, seus dados vão ficar publicos apenas se você liberá-los explicitamente, não por alguma bestera ou mal entendido.

### Pontos negativos

Falado de como pode passar a utilizar o Gitlab, vou primeiro tacar o pau nas coisas que não gosto ou sentirei falta em relação ao Github para só depois trazer os pontos que julgo bastante positivos.

#### Interface

Bem, não é segredo que a interface do Gitlab é completamente diferente da do Github. E em questão de usabilidade tem as coisas menos óbvias, minha impressão. Portanto, imagino que para se adaptar a essa interface será um pouco ruim (por mais que ela tenha melhorado bastante de uns anos para cá - primeiras vezes que usei Gitlab), ainda mais vindo de um sistema que tinha isso tão bem trabalhado.

Mas vejo que é o preço a se pagar... Gitlab tem a ideia de colocar tudo num pacotão, entregando um registry docker, ci/cd, vsc, tudo nesse mesmo pacote/interface, portanto, ficar cheia de conteúdo assim é algo que se espera.

#### Rede social

E, pelo menos para mim, perde completamente o sentimento de estar em uma rede social. O Github implementa essa ideia de criar uma "rede social para programador" (foi assim que o sistema me foi apresentado e, quando volta e meia minha vó me pergunta o que é o Github, é assim que eu respondo).

Interessante que, pelo menos para mim, isso realmente funcionava. Eu passava mais tempo navegando no Github, vendo atividades da galera, descobrindo novos projetos interessantes, do que em outras redes sociais como Facebook.

Infelizmente essa é uma feature que vejo ser complicada de ser implementada, principalmente pela necessidade que o Gitlab busca cobrir, que são completamente diferentes.

### Pontos positivos

Agora vamos para a parte boa, que tal???

#### Docker registry

A primeira vez que utilizei essa feature foi cerca de dois anos atrás, em 2016, e ela já funcionava lindamente!

Basicamente, você tem a possibilidade de subir imagens Docker para o registry de algum repositório no Gitlab. Não estou falando de subir o Dockerfile e colocar no hub.docker.com, estou falando de colocar a imagem no [Gitlab Container Registry \[7\]][7] MERMO!

Isso é bastante útil quando você pensa em integrar práticas DevOps em seu trabalho. Realmente, sensacional! Minha experiência com essa feature foi tudo de bom!

#### CI/CD

Pois bem, ainda tem isso, de forma integrada diretamente com o Gitlab. Como já falei, a ideia aqui é ter um pacote de ferramentas, todas altamente integradas já. Para incrementar ainda mais a vida do profissional de tecnologia nos dias de hoje, Gitlab integrou essa [feature de CI/CD \[8\]][8] aos repositórios.

Minhas experiências com essa feature foram boas. Não houve demora, coisa de alguns minutinhos.

Algo que gosto de salientar quando converso sobre esses builds é a respeito do ambiente que está sendo rodado esse shell emulado, algo que vi e achei interessante a preocupação na [palestra ShellScript Moderno, do Aurelio.net \[9\]][9].

#### Sites estáticos

E sites estáticos, eim?! O Github veio pra cá, todo bonitão, aceitando Jekyll e fazendo o Github Pages se proliferar no mundo. Daí veio o Gitlab e colocou para jogo VÁÁÁRIOS outros geradores de sites estáticos no [Gitlab Pages \[10\]][10].

O bom é que ainda melhorou drasticamente!! Sério! Lembro que quando fomos colocar o site do [LampiãoSec \[11\]][11], por volta de setembro de 2015, desistimos de colocar no Gitlab Pages e aceitamos migrar para o Github pelo parto que era fazer aquele negócio funcionar. Quem diria que aquila feature estranha, sem fluxo aparente, se tornaria essa belezura que é hoje eim?! Pois é!

Um ponto positivo massa que acho sobre isso é que o Gitlab oferta agora que os desenvolvedores trabalhem com menos trabalho com outros geradores de site estático, uma vez que a questão do agnosticismo do Github não era tão evidente nesse sentido. :P

Agora um ponto negativo que vi comentar sobre isso é que o rankeamento da página é muito pior no Gitlab pages que no Github pages. Presumi que isso seria pela maturidade e uso dessa feature. Veja, coletei alguns dados relacionados ao pagerank a respeito dos domínios github.io e gitlab.io:

| Domínio | Google PageRank | cPR Score | External Backlinks | EDU Backlinks | Gov Backlinks | 
| Github.io | 4/10 | 4.5/10 | 479,047,259 | 4,485,859 | 616,115 |
| Gitlab.io | 2/10 | 2.1/10 | 827,841 | 1,681 | 91 |

Esse é o tipo de coisa que só será melhorado conforme acreditarmos nisso e passarmos a usar cada vez mais ^^

#### Gerenciamento

Como disse, tenho mais experiência em projetos no Github que no Gitlab. Lá realmente realizei projetos de desenvolvimento, com entregas definidas, alta interação de equipes, ferramentas, técnias, tecnologias... enfim, quando trabalhei com esse tipo de coisa, foi no Github. Aqui no Gitlab apenas fiz alguns testes ou trabalhei em projetos pessoais ou no máximo em duplas.

Entretanto, já ouvi falar muitíssimo bem das ferramentas que o Gitlab disponibiliza para gerenciamento de projetos e equipes, e no meu uso particular, elas realmente funcionam bem. Inclusive, dá uma olhada [nesse post \[12\]][12] que o pessoal do Gitlab fez mostrando uma maneira de se organizar utilizando o sistema. Achei massa!

#### Outras

Por fim, lembrando que essas são apenas algumas das features que me fizeram gostar tanto do Gitlab e querer passar a usar mais o sistema. Uma lista mais completa você pode ver na [documentação oficial \[\]][].

## Agradecimento

Deixo aqui meu agradecimento à [Marino](https://github.com/Marinofull) que basicamente falou "Man, faz um post no Medium explicando porque não será doloroso migrar tudo pro gitlab, e fala dos diferenciais!".

Só preferi fazer aqui mesmo, mas é isso aí :D

No mais, obrigado a todos por terem lido. Qualquer coisa, interage aí, só mandar e-mail ou comentar aqui abaixo. Abração!

## Links

~~~

~~~

[0]: {{ site.url }}{{ site.baseurl }}posts/consequencias-bloqueio-whatsapp/
[1]: https://blog.github.com/2018-06-04-github-microsoft/
[2]: https://news.microsoft.com/2018/06/04/microsoft-to-acquire-github-for-7-5-billion/
[3]: https://medium.com/swlh/please-dont-do-it-github-5890eb72d12c
[4]: https://about.gitlab.com/2018/06/03/microsoft-acquires-github/
[5]: {{ site.url }}{{ site.baseurl }}tips/blog-no-gitlab-pages/
[6]: https://gitlab.com/users/sign_in
[7]: https://about.gitlab.com/2016/05/23/gitlab-container-registry/
[8]: https://about.gitlab.com/features/gitlab-ci-cd/
[9]: https://www.youtube.com/watch?v=XBkBnKmu94U
[10]: https://about.gitlab.com/features/pages/
[11]: https://lampiaosec.github.io
[12]: https://about.gitlab.com/2018/02/08/using-gitlab-to-manage-house-renovation-priorities/
[]: https://about.gitlab.com/features/