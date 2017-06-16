---
layout: post
title:  "Compartilhando o termial - ShellShare &amp; Asciinema"
date:   2015-10-24 11:16:49
categories:
    - tips
tags:
    - linux
    - terminal
    - cli lindo!
---

## Introdução

Muitras vezes queremos passar o passo-a-passo de algo para um amigo ou demais pessoas e é simplesmente seguir utilizando o terminal e explicando onde for necessário. Gravar toda a tela com programas como Kazam, Record My Desktop e similares é uma opção, mas talvez não das melhores, ainda mais se você preza por sua RAM. haha<!--more-->



Pensando nisso surgiu o ShellShare [1], um projeto do Vitor Baptista, aberto e hospedado no Github. Como o próprio nome já informa, é um software responsável para fazer o compartilhamento do terminal, falarei melhor mais adiante.

Além desse ShellShare - que é como um live do terminal - tem o Asciinema [2] que grava o terminal e deixa online como um vídeo à seu dispor.

Vou fazer duas sessões nesse post: uma sobre o ShellShare e uma sobre o Asciinema, então, eles se completam.

## ShellShare

Na própria descrição do projeto é mostrado para o que foi feito, simplesmente: compartilhar o terminal. Apenas como um broadcast, ou seja, quem estiver assistindo não poderá controlar seu computador atravéz deste.

### Instalação

A instalação é muito simples, basta fazer download do binário e ter Python em seu computador. Difícil, não?!

~~~
gjuniioor@lampiaosec > wget -qO shellshare http://get.shellshare.net
~~~

> A opção `-q` do `wget` faz com que não haja saída em tela do comando, e a `-O` determina qual o nome do arquivo baixado.

Depois disso, basta dar permissão de execução para ficar melhor utilizável e mover para um caminho do Path, se assim quiser.

~~~
gjuniioor@lampiaosec > chmod +x shellshare
gjuniioor@lampiaosec > echo $PATH
gjuniioor@lampiaosec > sudo mv shellshare /usr/bin
~~~

### Uso

Depois disso feito, o programa já pode ser utilizado em qualquer lugar do computador. Portanto, basta executar o comando e irá retornar um link. Esse link você passa para quem deve visualizar o compartilhamento e seja feliz!

Para finalizar a execução do ShellShare, use o comando `exit` ou tecle `ctrl+d`.

Para fazer um melhor uso, utilize a opção help:

~~~
gjuniioor@lampiaosec > shellshare --help
usage: shellshare [-h] [-v] [-s SERVER] [-r ROOM] [-p PASSWORD]

Transmits the current shell to shellshare

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -s SERVER, --server SERVER
                        shellshare instance URL (default: shellshare.net)
  -r ROOM, --room ROOM  room to share into (default: random room)
  -p PASSWORD, --password PASSWORD
                        room's password (default: random password)
~~~

Perceba as opções `-r` e `-p`, são minhas favoritas. Utilizando elas você pode utilizar uma sala de sua escolha e configurar uma senha, para somente quem a tiver poder acessar. Bacana, não?!

## Asciinema

Já falei sobre ele, não há muito o que acrescentar, simplesmente: grava o terminal e disponibiliza na web por um player em js.

### Instalação

Não preciso explicar muito essa parte, já é bem documentada no próprio site do projeto: [3].

Em suma, provavelmente está nos repositórios de sua distribuição.

### Uso

Basta rodar o comando de gravação:

~~~
gjuniioor@lampiaosec > asciinema rec
~~~

Após isso vai começar gravar. Para finalizar, digite o comando `exit` ou pressione `ctrl+d`.

Automaticamente, após a finalização, vai perguntar se você quer fazer upload, pressionando sim, em instantes irá retornar um link onde poderá assistir à gravação. Por enquanto, esse usuário não está registrado, ou seja, tu não poderá editar nada após isso. 

Mas temos uma solução! Execute o comando: 

~~~
gjuniioor@lampiaosec > asciinema auth
~~~

Que ele vai te passar um link para acessar pelo browser. Após isso, basta inserir e-mail, verificar... Ou seja, basta seguir um procedimento "next like".

Assim como recomendei para o ShellShare, para o asciinema, é bom olhar o help dele para ter uma noção de novas opções.

~~~
gjuniioor@lampiaosec > asciinema --help
usage: asciinema [-h] [-y] [-c <command>] [-t <title>] [action]

Asciicast recorder+uploader.

Actions:
 rec              record asciicast (this is the default when no action given)
 auth             authenticate and/or claim recorded asciicasts

Optional arguments:
 -c command       run specified command instead of shell ($SHELL)
 -t title         specify title of recorded asciicast
 -y               don't prompt for confirmation
 -h, --help       show this help message and exit
 -v, --version    show version information
~~~

Como por exemplo a opção `-t` que já configura o cast na web com um título.

## Conclusão

Bem, basicamente, é isso! São duas ótimas formas de compartilhar o terminal, sem precisar de um pesado Recorder My Desktop ou um sugador como um Hangouts.

No mais, have fun e até mais ver!

## Referências

~~~
[1] - https://github.com/vitorbaptista/shellshare
[2] - https://asciinema.org/
[3] - https://asciinema.org/docs/installation
~~~
