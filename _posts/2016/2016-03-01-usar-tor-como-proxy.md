---
layout: post
title:  "Dica Rápida :: Usar Tor como proxy (no IRC)"
date:   2016-03-01 17:00:00
categories:
    - tips
tags:
    - archlinux
    - dicas
    - privacidade
    - redes
    - seguranca
    - tor
---

E mais uma dessas dicas rápidas, vambora??

Agora vou mostrar como você pode utilizar a rede tor para servir de proxy. Como exemplo, vou utilizar o IRC como exemplo, com os clientes hexchat e weechat (esse já tenho um post mostrando [como usar aqui \[0\]][0]). Tudo isso, no lindo [ArchLinux \[1\]][1].

## Instalação

Primeiro passo: Instalação do Tor.

É uma coisa bem simples, afinal, utilizamos GNU!

* ArchLinux: $ sudo pacman -S tor --noconfirm
* Debian: $ sudo apt-get install tor -y

## Inicialização

Depois, vamos precisar rodar o daemon do tor para poder utilizá-lo como proxy. Isso também é simples, vejamos alguns comandos:

~~~
$ systemctl status tor.service
~~~

Esse ai vai ver o status atual do serviço. Como não iniciamos ele, vai mostrar inativo. O próximo comando é para colocar o tor para rodar:

~~~
$ sudo systemctl start tor.service
~~~

Se você quiser parar o serviço, basta mudar o **start** por **stop**.

Caso queira colocar o daemon do Tor para já iniciar junto com a inicialização do sistema, basta habilitar esse serviço:

~~~
$ sudo systemctl enable tor.service
~~~

E por fim, se quiser parar com isso:

~~~
$ sudo systemctl disable tor.service
~~~

## Configuração do proxy

Se você passar o nmap em seu computador verá que tem a porta 9050 aberta. Pois é nela que o Tor roda. E o proxy que vamos utilizar é com o protocolo SOCKS5. Essas são as informações que você precisa para utilizar em qualquer lugar.

Antes de colocar no IRC, vamos fazer alguns testes... Por exemplo, veja qual teu IP:

~~~
$ curl http://ifconfig.me
~~~

E depois olhe o IP utilizando o proxy:

~~~
$ curl --proxy socks5://127.0.0.1:9050 http://ifconfig.me
~~~

Duas observações:

1. Veja que seu IP mudou. Se não mudou, há algo de errado. Veja se realmente subiu o serviço do Tor.
2. Note que vai demorar mais. Claro, afinal, vai passar pelos servidores do Tor e isso requer mais saltos.

Então, vamos recapitular as informações que você precisa para configurar o proxy em qualquer lugar:

* Servidor: seu computador, 127.0.0.1
* Porta: 9050
* Protocolo: socks5

## Configuração do Hexchat

Não vou colocar prints aqui por <del>preguiça</del> alguns motivos mas basta seguir como falado aqui que funciona. Ao menos na versão 2.10.2.

1. Clique em **Configurações** >> **Preferências**
2. Nessa janela, pelo menu da esquerda, vá em **Rede** >> **Configurações de Rede**
3. Terá uma parte referente a **Servidor Proxy**, coloque as informações obtidas na seção anterior ai
4. Reconecte
5. Seja feliz!

Simples, não?!

## Configuração do Weechat

> Antes de mais nada, se você não sabe utilizar o Weechat, recomendo que leia [esse post\[0\]][0].

No Weechat, você terá de fazer uma configuração de proxy primeiro e depois adicionar esse proxy já configurado ao servidor que deseja utilizar. Vejamos:

Primeiro, vamos criar a configuração do proxy:

~~~
/proxy tor socks5 127.0.0.1 9050
~~~

E depois, só colocar no servidor que desejar:

~~~
/set irc.server.oftc.proxy tor
~~~

E então, basta reconectar!

> Claro, mais importante que ver como fazer é entender um pouco mais o processo. Falo isso sobre o Weechat e deixo aqui a sugestão de utilizar o help dele para ver mais opções:

~~~
/help proxy
/help server
~~~

## Flws!

Bem, como mostrei, é uma dica rápida. Então, até mais ver!

## Links

~~~
[0]: {{ site.url }}{{ site.baseurl }}blog/weechat/
[1]: {{ site.url }}{{ site.baseurl }}category/#archlinux
~~~

[0]: {{ site.url }}{{ site.baseurl }}blog/weechat/
[1]: {{ site.url }}{{ site.baseurl }}category/#archlinux
