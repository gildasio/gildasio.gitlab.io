---
layout: post
title:	"Arch Linux + XFCE = Clean"
date:	2016-01-17 21:00:00
categories:
    - tips
tags:
    - archlinux
    - linux
    - screenshot
---

![Screenshot]({{ site.baseurl }}images/posts/2016/02.jpg)

> Caso queira ver o print maior, [clica aqui \[0\]][0].

Screenshot mostrando cena do filme *"Efeito Dominó"* (ou *The Bank Job*), também com uminstância do terminal utilizando o programa *screenfetch* para algumas informações do sistema. Como shell estou utilizando o ZSH. Utilizo um tema nele, caso esteja interessado, aqui:

~~~
PROMPT=$'%{$fg_bold[cyan]%}%~%{$fg_bold[white]%}$(git_prompt_info) %{$fg_bold[cyan]%}%D{[%I:%M:%S]}\
>%{$reset_color%} '

ZSH_THEME_GIT_PROMPT_PREFIX=" %{$fg[white]%}("
ZSH_THEME_GIT_PROMPT_SUFFIX=")%{$reset_color%}"
ZSH_THEME_GIT_PROMPT_DIRTY="*"
ZSH_THEME_GIT_PROMPT_CLEAN=""
~~~

Dessa vez decidi fazer algo mais leve e menos *dark* como normalmente faço. Segue ai então um [wallpaper mais zen \[1\]][1], por exemplo.

> No print não deu para ver, mas estou utilizando [esse pacote \[2\]][2] para o cursor do mouse.

## Links

~~~
[0]: {{ site.baseurl }}images/posts/2016/02.jpg
[1]: {{ site.baseurl }}images/posts/2016/03.jpg
[2]: http://gnome-look.org/content/show.php/ComixCursors?content=32627
~~~

[0]: {{ site.baseurl }}images/posts/2016/02.jpg
[1]: {{ site.baseurl }}images/posts/2016/03.jpg
[2]: http://gnome-look.org/content/show.php/ComixCursors?content=32627
