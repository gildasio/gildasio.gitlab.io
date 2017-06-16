---
layout: post
title:  "A Pós Instalação do Arch Linux"
date:   2015-08-12 11:16:47
categories:
    - posts
tags:
    - linux
    - archlinux
---

Olá pessoALL!! Nesse artigo vou mostrar como é o processo de pós instalação do **Arch Linux**. Ao menos, da forma que eu uso... Alguns pode se perguntar o motivo de eu não tratar a instalação em si. Simples, já tem bastante coisa sobre isso. Se quiser, basta seguir um punhado de comandos que podem ser encontrados por toda a internet e pronto. Uma pós instalação é algo pessoal, que varia a depender do gosto das pessoas, então, esse meu post pode até servir para automatizar caso eu precise fazer novamente esse procedimento. :)

## A distribuição

Arch é uma das grandes distribuições GNU/Linux que existem. Numa primeira visão, é tida como uma distribuição complicada de se usar, mas nada que alguns instantes de leitura, quando se pega um problema, não resolva. Essa distro é focada em ser minimalista, elegante e, claro, muito **KISS**! Assim como o grandíssimo Slackware (Amém!).

<!--more-->

Ela tem seu próprio *package manager*, o **Pacman**, que particularmente, é o melhor que já utilizei. Fora os repositórios oficiais e do Pacman, tem o **AUR** (Arch Linux User Repository) que contém alguns scripts que automatizam a instalação de bastante coisa. Pode ser pensado como um SlackBuilds, para quem conhece.

Chega de enrolação, e vamos seguir...

## Pré-Requisitos

Como já deve ter percebido, esse é um post sobre Pós instalação, o que quer dizer que apenas o que precisa é do Arch instalado. Conexão com a internet já está incluso, para o caso das instalações...

## Leringou?!

Antes de mais nada, gostaria de salientar que todos esses comandos aqui mostrados foram testados em meu processo de pós instalação, mas se no caso de algum de vocês tiver algum erro, basta comentar e unimos forças para resolver.

#### Teclado

A primeira parte da configuração é deixar o teclado em ABNT2 permanentemente. Para isso, basta editar um arquivo inserindo um parâmetro... Simplesmente rode o comando:

~~~
# echo "KEYMAP=br-abnt2" >> /etc/vconsole.conf
~~~

Já vai estar lindamente configurado. Ou ao menos deveria... Vale lembrar que essa configuração de teclado é válida para o console. Caso rode um ambiente gráfico deverá fazer mais um procedimento (mas eu mostrarei quando chegar a hora).

#### Usuário

Se você usa GNU/Linux deve saber o motivo dele ser tão seguro. Mas se não sabe, vem com o tio... Se dá principalmente pelo "isolamento" de permissões que o usuário normal e o root tem. Então, precisamos criar nosso usuário... Veja o comando:

~~~
# useradd -m gjuniioor
~~~

Basta criar a conta, criando juntamente a pasta para esse usuário (isso se faz com o parâmetro `-m` ali mostrado). Depois, vamos nos atentar para com a senha. Mude-a:

~~~
# passwd gjuniioor
~~~

#### Sudo

Pronto, agora isolamos o root na dele para não ser muito usado (essa é uma ótima prática). Mas precisamos ter privilégio com o nosso usuário para que ele possa instalar programas, configurar certas coisas e demais. O `sudo` faz isso para você... Ele consegue fazer com que usuários que tenham permissão se torne o todo poderoso por um instante. Vamos instalar:

~~~
# pacman -S sudo
~~~

Depois disso, teremos de dar essa permissão ao nosso usuário. Há várias formas de se fazer isso... Abra o arquivo `/etc/sudoers` e ao final terá uma sessão para isso. A maneira que prefiro fazer é adicionando meu usuário ao grupo `sudo` e assim, tendo todo acesso.

Então, temos de criar o grupo e adicionar nosso usuário a ele:

~~~
# groupadd sudo
gpasswd -a gjuniioor sudo
~~~

E lá no arquivo de configuração que já mostrei (se não lembra, leia novamente, você está fazendo isso errado) podemos descomentar a linha que tem algo como `%sudo ALL=(ALL) ALL`.

#### Rede

É de suma importância se conectar à internet... Se você utiliza rede wifi, pode fazer isso de forma simples com o `wifi-menu`. Se você precisa de conexão cabeada, tem uns pares de tutoriais por ai ensinando sobre isso (inclusive na wiki do Arch, claro).

Agora, sempre que ligamos o computador teremos de rodar o `wifi-menu` ou seja lá qual programa use para se conectar? Claro que não... Basta dizer ao sistema para sempre que ligar já buscar pelas redes que já fez login. Apenas execute:

~~~
$ ip addr
~~~

Com esse comando saberemos os nomes das nossas interfaces de rede (já que o padrão foi alterado e ainda não encontrei um motivo bacana para isso ou uma forma legal de reverter) que iremos usar para o comando, veja:

~~~
systemctl enable netctl-auto@interface_wifi
systemctl enable netctl-ifplugd@interface_ethernet
~~~

#### Yaourt

Já falei sobre o **AUR** aqui. O `yaourt` é basicamente um "Pacman" que vai utilizar esse repositório. Bacana, não?! Vamos instalar ele...

Abra o arquivo `/etc/pacman.conf` e insira isso ao final:

~~~
[archlinuxfr]
SigLevel = Never
Server = http://repo.archlinux.fr/$arch
~~~

Em seguida, atualize a lista dos servidores e instale o programa:

~~~
# pacman -Sy
# pacman -S yaourt
~~~

#### Xorg

Como nem do de linha de comando vive o homem, talvez precisaremos do X instalado e rodando. Então, vamos ver o que fazer... O primeiro passo sobre isso é instalar os servidores e demais programas necessários.

~~~
# pacman -S xorg xorg-xinit
~~~

Pronto, já está ok! Ao menos o servidor... Agora precisaremos do *window manager* ou um *desktop eviroment* se preferir.

###### Teclado para o X

Eu disse que quando chegasse o momento eu falaria. Já que instalou o servidor é porque vai rodar ambiente gráfico em algum momento. Então, precisará do teclado devidamente configurado quando for usar isso... Basta editar o arquivo `/usr/share/X11/xorg.conf.d/10-evdev.conf` adicionando isso:

~~~
Section “InputClass”
Identifier “evdev keyboard catchall”
MatchIsKeyboard “on”
MatchDevicePath “/dev/input/event*”
Driver “evdev”
Option “XkbLayout” “br”
Option “XkbVariant” “abnt2"
EndSection
~~~

X pronto, prosseguimos!

#### i3 Window Manager

Seguindo a ideia de que o Arch é uma distro minimalista (e eu adoro isso) o i3 é um window manager de alta qualidade, simples de configurar, leve... Ou seja, se viesse com pizza seria perfeito! Vamos instalar ele:

~~~
# pacman -S i3 dmenu
~~~

OBS: O i3 usa o `dmenu` como um laucher, então, é legal ter para facilitar a vida.

Agora, adicione a linha para executar o i3 ao iniciar o x: `echo "exec i3" > ~/.xinitrc`.

Para rodar basta chamar o `startx`.

Possa ser que precise de um terminal quando vai para o X, então, recomendo a instalação do Xterm: `pacman -S xterm`.

Não vou mostrar aqui como personalizar o i3 pois já tem um material muito bom que passarei a você. Recomendo que termine esse post para depois prosseguir para o do i3: [Link User Guide](http://i3wm.org/docs/userguide.html). Deixo aqui também a sugestão dos meus arquivos de configuração: [Github](https://github.com/gjuniioor/i3wm-files).

#### Áudio

Vamos deixar o áudio funcionando para caso precisemos daquela empolgação com a música... Precisamos então do `alsa` e do `pulse` trabalhando lindamente. Vamos:

~~~
# pacman -S alsa-lib alsa-utils alsa-firmware alsa-plugins pulseaudio-alsa pulseaudio
# pacman -S pamixer
# pacman -S cmus vlc
~~~

A primeira linha instala os programas necessários para rodar o som. A segunda é um mixer via linha de comando que eu decidi testar e estou gostando. E na terceira, já dá para perceber que se trata de reprodutores, certo?! O `cmus` é um reprodutor de áudios feito para CLI. O `VLC` dispensa apresentações.

Talvez você precise adicionar para o `pulseaudio` ser executado ao iniciar o i3. Talvez não... De qualquer forma, teste, se precisar, basta fazer isso:

~~~
$ echo 'exec --no-startup-id "pulseaudio --start' >> ~/.i3/config
~~~

Para adicionar um ícone informando sobre o status do volume, pode configurar mexendo em um arquivo (e o guia do i3 mostra como) ou pode simplesmente copiar meu arquivo de configuração para você: [Github](https://github.com/gjuniioor/i3wm-files).

#### Programas usuais

Irei adicionar aqui alguns programas que são importantes e bastante úteis se ter... Os softwares contidos aqui são de minha escolha pessoal, ou seja, são que eu gosto, fique a vontade para preencher como quiser. Vejamos:

###### Compressores

~~~
# pacman -S tar gzip bzip2 unzip unrar p7zip
~~~

###### Browser

~~~
# pacman -S luakit firefox
~~~

###### Compatibilidade de disco

~~~
# pacman -S ntfs-3g dosfstools
~~~

###### Downloaders

~~~
# pacman -S wget curl
~~~

###### PDF Viewer

Gostaria de comentar sobre essa seção em especial... Tem uma aplicação para leitura de PDF no modo gráfico que é bem leve e gosto dela:

~~~
# pacman -S epdfview
~~~

Mas as vezes me dá na telha a vontade de usar o console puro. Portanto, as vezes leio pdf por ele. Então, é preciso o programa `fbgs` que está no pacote `fbida` para rodar. Então:

~~~
# pacman -S fbida
~~~

Mas ele precisa de um outro (o famoso `ghostscript`) para gerar o que você vai visualizar:

~~~
# pacman -S ghostscript
~~~

###### Demais

~~~
# pacman -S bash-completion
~~~

Com esse programa, ele já configura automaticamente o autocomplete ao pressionar TAB de diversos comandos, como `man`, `info`, `whereis` e demais...

## Conclusão

Então pessoal, é isso... Tem mais coisas que uso, claro!, como por exemplo o Vim, Transmission... Mas isso fica para outros posts pois são mais extensos e aqui está o básico para deixar funcional e já redondo. Fiquem a vontade para criticar se quiserem.

Não deixem de ver meus dotfiles no [Github](https://github.com/gjuniioor) para caso queiram usar eles.

Até mais ver!

## Update

- Inserido o pacote `dosfstools` na seção relacionada a compatibilidade de discos. Com ele, é possível formatar partições com o padrão FAT.

- Adicionada a seção *Demais* que cita programas extras que são bem úteis para uso de forma geral.

- Corrigido o nome do arquivo de `~/.xinit` para `~/.xinitrc`. Obrigado, <a href="http://www.vivaolinux.com.br/~z3lost" target="_blank">z3lost</a>, pela observação!
