---
layout: post
title:  "Contribuindo Para Projetos Abertos no Github"
date:   2015-07-30 11:16:47
categories:
    - posts
tags:
    - programacao
    - git
---

O título desse post já é bem descritivo, mas para ser mais claro, vou deixar algumas coisas clara antes de mais nada:

### O que é esse artigo

Aqui eu irei comentar sobre os benefícios de contribuir para projetos abertos e utilizando o Git, formas de fazer isso e como fazer. Para nosso estudo de caso utilizarei o Github como servidor (por conta da quantidade de projetos que por lá estão e tudo mais).

### O que não é esse artigo

**Não é um tutorial sobre Git!**

Para isso, leia a documentação no [site do projeto](https://git-scm.com/doc) ou simplesmente, *Google is your friend*! :)

<!--more-->

## Benefícios

Agora, podemos começar o artigo em si... Quero falar logo sobre os benefícios de você ajudar em projetos alheios.

Veja bem, todo o projeto GNU/Linux é o que é hoje em dia graças à colaboração que muitas pessoas fizeram para que ele ficasse dessa forma. Então, pense no benefício que não é para a comunidade se você a ajuda a crescer mais e mais!!

Além do benefício comunitário envolvido, tem mais. Principalmente o autodesenvolvimento! Você vai praticar o uso das tecnologias que tem interesse, vai aprender a atuar melhor em equipe e também utilizar o Git - que é o software mais utilizado hoje em seu ramo. Fora que se/quando chegar o momento de uma entrevista de emprego (já tem muitos casos assim) você pode mostrar sua experiência para a empresa apenas linkando seu perfil para eles.

Convenci que é uma boa ajudar? Se sim, segue, se não, lê novamente haha.

## Maneiras de contribuir

Para ajudar em um projeto você não precisa ser fera em um assunto! Afinal, muitas das vezes, é ajudando que você vai aprendendo mais e mais. Portanto, o único pré-requisito para ajudar é a vontade!!!

Tem várias opções de formas de ajudar, vejamos:

#### Programação

Se você entende da linguagem que o projeto é feito você pode meter a mão no código e corrigir bugs que tenha, inserir novas funcionalidades e resolver *issues* que sejam listadas.

Novamente lembrando, não é necessário que você seja um expert na tecnologia! Sempre que você manda alterações, elas serão analisadas. Portanto, se forem boas, serão aceitas, se não, o autor pode (e provavelmente vai) te dar dicas de onde melhorar.

#### Criando issues

Você pode pensar em algo interessante que o projeto poderia ter ou encontrou algum bug (mínimo que seja) no programa. Bacana! Fale sobre isso na parte direcionada à issues do projeto. Nessa parte, tente ser o mais claro possível e com bastante informações.

> O Github - e vários de outros servidores - aceita a sintaxe de escrita em *markdown*, portanto, pode usar dela para escrever o conteúdo mais organizado e arrumado de forma mais fácil.

#### Tradução

O projeto é somente em inglês e acha que poderia ser legal tê-lo em português (ou o contrário)? Traduz ele! Simples assim... E não estou falando apenas do software em si, mas pode pensar em traduzir a documentação, FAQ e outros materiais que seja útil para ele.

#### Documentação

Muitas vezes quando se é feito um projeto, o autor cria a documentação com muito cuidado e deixa-a disponível. Mas conforme o programa vai crescendo, ou ele abandona e deixa de fazer a documentação ou apenas esquece disso. Portanto, fique a vontade para atualizar.

Ou então, testar todos os exemplos se realmente funcionam e adicionar como resolver caso não. Inserir procedimentos para, por exemplo, instalação em uma gama maior de sistemas operacionais... E por ai vai!

## Mão na Massa

Achou sua forma de contribuir? Ótimo! Vejamos como fazer isso...

> **P.S.:** Para exemplos, pegarei o programa [Virgulino](https://github.com/lampiaosec/virgulino), projeto feito pelo grupo de pesquisa em segurança [LampiãoSec](https://lampiaosec.github.io), que é um experimento para estudos relacionados à esteganografia.

> **P.S.S.:** Vou assumir que já tenha conta no Github (caso não tenha, faça) e que tem o Git instalado em sua máquina com o mínimo já configurado (bem, há vários posts ensinando como fazer isso, caso precise).

#### Fork

O primeiro passo é encontrar o projeto com que contribuir. Como disse, pegarei como exemplo o [Virgulino](https://github.com/lampiaosec/virgulino), link do repositório: https://github.com/lampiaosec/virgulino.

Depois de escolhido, como, provavelmente, você não terá acesso à edição direta no projeto, você deverá fazer um `fork` que consiste basicamente em criar uma cópia do mesmo. Para isso, na página do projeto, clique no botão com esse nome.

Agora que já tem o projeto copiado em sua conta, acesse o repositório em seu nome. Basta alterar a url com seu nome de usuário no lugar de `lampiaosec`, ficando algo como [https://github.com/seu_usuario/virgulino](#).

#### Clone

Feito isso, agora precisamos de ter o código em nossa máquina para edição, certo? Basta clonar o repositório:

~~~
$ git clone https://github.com/seu_usuario/virgulino
~~~

Entre no diretório do repositório e já pode começar a editar.

> Nota: Já disse que aqui não é um tutorial sobre Git, logo, não vou mostrar como adicionar arquivos ao stagement, como fazer `commit`, `push` e etc.

#### Pull Request

Depois de você ter alterado tudo que queria, fazendo os passos de adicionar as mudanças e subido para seu fork, você pode submeter essas suas alterações para que fique no projeto original. Para isso, vamos fazer um *Pull Request*!

> Outra nota: O Github chama isso de *Pull Request*, mas em outros servidores você pode encontrar como *Merge Request* ou variantes.

Estando logado e acessando ou o seu repositório ou o oficial do projeto, verá um botão na cor verde. Ele representa esse *Pull Request*. Clique nele e irá aparecer um formulário para você... Nesse formulário, você deve descrever as alterações que fez, facilitando um pouco a vida de quem vai analisar a requisição. Opcionalmente, se foi o caso, você pode "linkar" com as issues que tenha relação, apenas colocando o número a que ela se refere.

#### Atualizando o fork

Normalmente, quando você começa ajudar um projeto, você faz isso diversas vezes. Logo, pode dar uma ajuda hoje, uma amanhã e até no mês que vem. Isso não indica que o projeto será sempre o mesmo, sem mudanças além das suas. Ou seja, você precisa atualizar o que tem em sua máquina.

Para fazer isso, temos a opção simples e a opção certa. Vamos ver:

###### Simples

01. Remova o diretório do projeto
02. Clone o projeto novamente

Nada bonito isso, né?!

###### Certo

Primeiro, adicione o link do repositório oficial ao seu repositório local:

~~~
$ git remote add upstream https://github.com/lampiaosec/virgulino
~~~

> **Mais uma nota:** O nome *upstream* é apenas uma convenção que se foi criada. Ou seja, boas práticas... Mas isso não te impede de inserir um nome diferente, como *link_dos_cara*.

Agora, basta atualizar usando o comando `git pull` e seja feliz.

Ah!! Lembre-se de fazer essa atualização antes de começar a mexer no projeto! Sério, isso te livra de dores de cabeça kkkk.

## Finalização

Bom, é isso! Talvez, posteriormente eu faça posts mostrando funcionalidades e como utilizar o Git (para não passar batido em alguns pontos), mas por enquanto, pronto! Não tem desculpas para usar dizendo que não sabe ajudar nesses projetos.

Espero que vire um contribuinte assíduo!

Até mais ver! :D
