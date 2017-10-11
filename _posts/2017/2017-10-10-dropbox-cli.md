---
layout: post
title:	"DropBox Command Line"
date:	2017-10-10 23:00:00
categories:
    - tips
tags:
    - cli lindo!
    - debian
    - dicas
    - dropbox
    - linux
---

Olá, pessoas e demais! Há um tempo que não posto nada por aqui... Acontece. Estou tentando me organizar para poder trazer mais coisas e popular aqui um pouco mais, nem que seja com posts nessa pegada, de ser mais uma dica, nada tão trabalhoso. O difícil é só encontrar alguma coisa que possa fazer isso e não ser mais do mesmo. Mas vamos lá ...

Quem já deu as caras por aqui pelo blog já deve ter reparado que curto um pouco essa [coisa de linha de comando \[0\]][0]. Acho legal, utilizar o computador basicamente só digitando textos. Além de ter um desempenho mais interessante e tornar a pessoa quase um poliglota, já que os comandos seguem um padrão e tudo mais. Enfim.

Recentemente precisei arrumar do zero uma máquina aqui. Com isso quero dizer instalar as coisas que fossem necessárias: SO, drivers, aplicativos, essas coisas. Uma delas é Dropbox. Interessante você poder fazer essa coisa de backup de alguns arquivos assim e tê-los acessíveis de vários locais, certo? Pois bem.

Um tempo atrás eu utilizava o [MeoCloud \[1\]][1]. É um serviço português. Algo como o Dropbox mesmo. Tem alguns diferenciais, claro. Entre eles um player de mídia que achava bem bacana. Mas o principal para mim era o cliente linha de comando que ele tem. Achava isso muito massa pois poderia configurar em servidores, desktops que só rodava linha de comando, enfim, várias coisas.

Acontece que tendo de fazer essas instalações recentemente acabei vendo que o Dropbox lançou algo assim por agora! Se minha memória não falha, antes, por mais que você instalasse tudo via linha de comando e fosse usar assim depois, para fazer a configuração inicial, de logar em sua conta e tudo mais, precisava de interface gráfica. Agora não mais!

Basta você vir [nesse link \[2\]][2]. Nele você terá algumas formas de instalação. Siga a que lhe for mais confortávei e fizer sentido com seu contexto. Lá para o final da página tem falando sobre o script em python que você pode baixar:

~~~
$ wget https://www.dropbox.com/download?dl=packages/dropbox.py
~~~

Depois você pode dar permissão de execução nele e colocar em algum diretório em seu `$PATH` e tudo certo, só

~~~
$ dropbox --help
~~~

E já foi! Já fui também, até mais! :P

## Links

~~~
[0]: {{ site.url }}{{ site.baseurl }}category/#cli lindo!
[1]: https://meocloud.pt
[2]: https://www.dropbox.com/install-linux
~~~

[0]: {{ site.baseurl }}category/#cli lindo!
[1]: https://meocloud.pt
[2]: https://www.dropbox.com/install-linux
