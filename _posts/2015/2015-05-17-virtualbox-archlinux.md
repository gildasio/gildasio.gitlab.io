---
layout: post
title:  "VirtualBox no ArchLinux"
date:   2015-05-17 11:16:47
categories:
    - tips
tags:
    - linux
    - archlinux
    - virtualbox
---

Arch Linux não é essa distribuição que é só chegar, rodar um comando e pronto... Pois bem, para aqueles que gostam de fazer seus testes, é interessante ter um ambiente de virtualização disponível. E uma ótima solução para isso é o VirtualBox.

Nesse artigo vou abordar os seguintes tópicos:
- Instalação
- Habilitando os módulos e rodando no boot
- Habilitando modos de rede Host Only e Bridged
- Adicionais para convidado
- Extension Pack
<!--more-->
## Instalação

A instalação é, de certa forma, simples. Primeiramente, terá de instalar o pacote VirtualBox:

~~~
# pacman -S virtualbox
~~~

Depois você precisará instalar os módulos. Mas antes, tem de saber qual o seu *kernel* e escolher o módulo relacionado à ele. Para saber a versão do *kernel* que você usa:

~~~
$ uname -r
~~~

Após rodar o comando acima, verifique qual é o *kernel* instalado por aí. Se for o ARCH:

~~~
# pacman -S virtualbox-host-modules-arch
~~~

Caso seja o *kernel* LTS:

~~~
# pacman -S linux-lts-headers virtualbox-host-dkms
~~~

E, por fim, para poder usar a interface gráfica mais comum, que é baseada no Qt, precisa instalá-lo:

~~~
# pacman -S qt
~~~

*P.S.*: eu não precisei, mas para evitar que aconteça algum problema contigo, melhor adicionar logo seu usuário ao grupo do VirtualBox (**Ah! Não preciso avisar para substituir "gjuniioor" pelo seu usuário, né?!**):

~~~
# gpasswd -a gjuniioor vboxusers
~~~

Com isso que fizemos até agora, já temos o essencial (referente à programas) para rodar o VirtualBox, mas ainda precisamos de uma coisinha... Siga.

## Habilitando Módulo

Isso mesmo! Para rodar o VirtualBox precisa-se rodar um módulo em específico, que é o "vboxdrv":

~~~
# modprobe vboxdrv
~~~

Possa ser que após fazer isso, a modificação não surta efeito. Então, você roda esse comando e certamente vai resolver:

~~~
# depmod -a
~~~

## Habilitando Módulos para rodar no Boot

Sempre que você iniciar seu computador, vai precisar rodar o módulo para poder usar o VirtualBox. Seria bom demais se tivesse como habilitar o módulo já no boot da máquina, né?! Pois bem! É possível! Veja...

Basta criar um arquivo em */etc/modules-load.d/*, pode ser com o nome "*virtualbox.conf*" mesmo:

~~~
# echo vboxdrv >> /etc/modules-load.d/virtualbox.conf
~~~

E pronto! Agora, sempre que iniciar a máquina, já terá o módulo rodando e com isso o VirtualBox vai rodar de boas.

## Habilitando Modos de Rede Host Only e Bridged

Até aqui, o que temos já pode rodar as máquias no modo de rede NAT e rede interna, mas pode ser que você precise rodar em Host Only ou Bridged e, para isso, precisamos fazer uns procedimentos a mais. Siga...

O Arch Linux não vem com o programa "*ifconfig*", mas sim com o "*ip*" (que é uma atualização). A questão é que o VirtualBox precisa dele para esses modos. O pacote que tem esse programa é o "*net-tools*". Então, só instalar, né?! Quase isso...

~~~
# pacman -S net-tools
~~~

Depois disso, vamos precisar rodar dois módulos:

~~~
# modprobe vboxnetadp
# modprobe vboxnetflt
~~~

*P.S.*: vamos ver se está lendo só por ler ou querendo aprender... Faça os passos já ditos anteriormente, para caso o carregamento do módulo não tenha surtido efeito e também habilite para rodar já no boot.

Depois disso, já é possível usar modo Bridged ou Host Only em nossas máquinas. Show!

## Adicionais para Convidados

Os adicionais para convidados permitem que o VirtualBox faça, por exemplo, compartilhamento de diretórios entre o Host e a VM, dentre outras coisas.

Para conseguir isso, precisamos instalar um complemento do VirtualBox:

~~~
# pacman -S virtualbox-guest-iso
~~~

## Extension Pack

O Extension Pack é um pacote de extensões que permite que o VirtualBox faça boot por placas Intel, ou ainda tenha acesso ao USB, por exemplo.

Para instalar, temos duas possibilidades. Vejamos.

#### Com AUR:

Basta executar o comando abaixo:

~~~
$ yaourt -S virtualbox-ext-oracle
~~~

#### Pelo VirtualBox:

Você precisará entrar nesse [link](https://www.virtualbox.org/wiki/Downloads) e importar o arquivo pelo menu: *Arquivo → Preferências → Extensões*.

### Observações

Esse artigo foi feito e testado no Arch Linux x86_64 com kernel 4.0.1-1-ARCH.

Foram testados os seguintes modos de rede: Bridged, Rede Interna e NAT.

Não cheguei a testar as opções de *Adicionais para Convidado* nem o *Extension Pack*, mas pela leitura de alguns manuais e Wikis, vi que seria dessa forma.

Todos os demais comandos foram testados.

Artigo originalmente postado no [Viva o Linux](http://www.vivaolinux.com.br/artigo/VirtualBox-no-Arch-Linux/ "Artigo no Viva o Linux").

Boa sorte e até mais ver! :D
