---
layout: post
title:  "Instalação do Arch Linux com LVM + Luks"
date:   2016-01-09 11:00:00
categories:
    - posts
tags:
    - archlinux
    - criptografia
    - hardening
    - linux
    - seguranca
---

* TOC
{:toc}

> *Engraçado* que já fiz um post falando sobre [a pós instalação do Arch Linux \[0\]][0] antes mesmo de fazer a instalação. Portanto, depois daqui, recomendo que dê uma olhada nesse outro post. :)

"Recentemente" foi encontrado um [bug no bootloader \[1\]][1] Grub, que pressionando backspace vinte e oito vezes resultava numa shell do Grub. Isso foi um reboliço danado na comunidade. A questão é que por se tratar de uma falha de exploração física, necessário ter acesso à máquina, "não precisa" dessa falha para uma possível invasão. Como com ela vai acontecer o reboot da máquina, você poderia fazer esse reboot manualmente e fazer o boot por um pen drive com um live CD, assim, vendo todos os arquivos da máquina.

E como quase sempre a solução para aumentar a sensação de segurança é recorrer à criptografia. Criptografar o disco, partições e arquivos nos deixa mais seguro quando se trata dessas coisas. Tendo essa perspectiva, aproveitei e juntei o útil (criptografar o disco) ao agradável (voltar ao usar o lindo Arch Linux) e aqui está o resultado de tudo isso.

### LVM + Luks

LVM (*Logical Volume Manager* - Gerenciador de Volume Lógico) permite gerenciar os discos com algumas funcionalidades interessantes, como por exemplo utilizar vários discos físicos para funcionar como um ou mais volumes, ou ainda poder remanejar o tamanho das partições e fazer toda essa gerência em tempo de execução.

LVM tem alguns conceitos bacanas a se abordar que guardarei para quando fizer um melhor sentido nesse texto. :) Se tiver interesse, recomendo a leitura de alguns links: [\[2\]][2], [\[3\]][3], [\[4\]][4], [\[5\]][5], [\[6\]][6] e [\[7\]][7]. E como são textos direcionados exclusivamente à LVM e não à implementação dele em uma instalação de um sistema, recomendo ainda mais para quem quer entendê-lo melhor.

Luks foi o que me motivou a fazer todo esse processo e por consequência, fazer esse post. Lembra que falei da criptografia do disco? Pois bem, ele quem vai permitir isso para a gente. Rapidamente falando, Luks é uma esecificação de encriptação de disco que veio para padronizar esse processo. Antes era utilizado de vários formatos diferentes, mas com o Luks isso foi resolvido. Vamos lá!

## Instalação

Vamos ver agora o passo a passo para a instalação do Arch Linux e claro com uso do LVM e Luks para tal.

### Teclado

O primeiro passo para você se sentir confortável por toda a instalação, já que se trata de um processo modo texto, é ter o teclado devidamente configurado. Para isso, basta executar:

~~~
# loadkeys br-abnt2
~~~

Se o teu teclado tem um outro formato, você pode ver os pamas no diretório */usr/share/kbd/keymaps/*.

### Internet

Vamos precisar da internet para fazer instalação dos pacotes ou para qualquer outra coisa que queira - como por exemplo: utilizar um script de instalação vindo do Github. :)

Para tal, basta executar o wifi-menu, selecionar a rede e colocar a senha:

~~~
# wifi-menu
~~~

#### Update

Um amigo me lembrou que não é só de wifi que vive o homem. Portanto, para conexão cabeada, você terá basicamente, de iniciar o DHCP após conectar o cabo:

~~~
# systemctl start dhcpcd
~~~

> Para mais informações leia [a página na Wiki do Archlinux sobre Redes Cabeadas \[8\]][8].

### Preparação dos Discos

Você pode utilizar qualquer programa para criar as partições da forma que quiser. Eu recomendo o *cfdisk*, mas fica a sua escolha.

Aqui vamos precisar apenas nos atentar algumas coisas:

* Não se deve criptografar o */boot*, senão o sistema não iniciaria;
* A partição de /boot vou utilizar com ext3, fica a seu critério. E deve ser marcada como bootável;
* A partição a ser utilizada pelo LVM tem de ter a flag "Linux LVM", ou se facilitar, o código 8e.

Pronto. Basicamente é isso. O esquema que escolhi fazer para mim foi o seguinte:

~~~
/dev/sda1 200MB       ext3       (vai ser utilizada para o boot)
/dev/sda2 (restante)  Linux LVM  (vamos separar aqui /, /home e swap)
~~~

### Encriptação

Antes de mais nada, vamos precisar carregar o módulo para utilizar o Luks:

~~~
# modprobe dm-crypt
~~~

E então vamos criptografar. Vou utilizar AES 512 para tal. Mas claro, fica a seu critério. Com intensão de não prolongar tanto, deixo com você para olhar as opções na *man pages* caso queira mudar:

~~~
# cryptsetup -c aes-xts-plain64 -y -s 512 luksFormat /dev/sda2
~~~

Depois de criptografado (note o *luksFormat*) vamos precisar abrir o disco para ser utilizado e preparado com o LVM para então formatá-los e todo o restante.

~~~
# cryptsetup luksOpen /dev/sda2 lvm
~~~

Vai estar disponível então em */dev/mapper/lvm*.

### Configurando LVM

Agora cabe a breve explicação que citei na seção sobre LVM. Ele trabalha com alguns conceitos interessantes, que são os PV (Physical Volume), VG (Volume Group) e LV (Logical Volume). Vamos entender melhor:

Você precisará dizer ao LVM qual dispositivo ele vai poder utilizar para fazer a abstração hardware-software. Esses são os PV, ou physical volume (volumes físicos). Vamos criando logo:

~~~
# pvcreate /dev/mapper/lvm
~~~

> Perceba que é o endereço dito mais acima, onde o disco está disponível para uso após abri-lo com Luks.

O VG ou grupo de volumes (Volume Group) vai ser responsável por agrupar volumes físicos, deixando disponível para criação das partições maiores que o tamanho dos discos físicos:

~~~
# vgcreate main /dev/mapper/lvm
~~~

> Dei o nome *main* ao grupo por convensão, mas como sempre alerto aqui, fica a teu critério.

LV ou volumes lógicos (Logical Volume) é, portanto, as partições lógicas criadas pelo LVM. Será nelas que as interações do kernel vão ocorrer e não mais diretamente no harware. Esse é o trabalho do LVM.

Tudo que precisará ser decidido é o tamanho das partições que deseja ter. Eu fiz o seguinte esquema:

~~~
/      20G
swap   6G
/home  restante
~~~

Se vai seguir a mesma configuração, os comandos ficam assim:

~~~
# lvcreate -L 20GB -n root main
# lvcreate -L 8GB -n swap main
# lvcreate -l 100%FREE -n home main
~~~

> Para ter melhor ideia dos wildcars disponíveis, veja a *man pages*.

### Formatação

Aqui já volta a ponto comum de qualquer instalação Arch. O que vai mudar é o endereço dos dispositivos:

~~~
# mkfs.ext4 /dev/mapper/main-root
# mkfs.ext4 /dev/mapper/main-home
~~~

E a criação da swap:

~~~
# mkswap /dev/mapper/main-swap
~~~

### Montagem

Vamos então montar os discos para prosseguir com a instalação:

~~~
# mount /dev/mapper/main-root /mnt
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot
# mkdir /mnt/home
# mount /dev/mapper/main-home /mnt/home
~~~

> Note bem como está organizado, com /, /boot e /home separados.

### Instalação

Agora é instalar o sistema base:

~~~
# pacstrap /mnt base base-devel
~~~

O Grub, a primeira parte, claro:

~~~
# pacstrap /mnt grub-bios
~~~

E gerar o fstab para "automatizar" a montagem das partições:

~~~
# genfstab -p -U /mnt > /mnt/etc/fstab
~~~

### Chroot

É o processo de mudar a raiz atual (do pen drive, CD, DVD, whatever) para a instalação recente. Basta fazer o seguinte:

~~~
# arch-chroot /mnt
~~~

> Vale ressaltar que se após você fizer a instalação, precisar utilizar novamente o pen drive para fazer alguma modificação no sistema, os únicos passos que precisará seguir é abrir o volume com Luks, montá-lo e fazer o chroot.

### Configuração

#### Locale

Abra o */etc/locale.gen* e descomente a linha que tem a informação sobre o idioma escolhido. Em meu caso "pt_BR.UTF-8 UTF-8".

Depois façamos:

~~~
# locale-gen
# echo LANG=pt_BR.UTF-8 > /etc/locale.conf
~~~

#### Senha do root

Basta alterar normalmente:

~~~
# passwd
~~~

#### Internet

Agora precisaremos instalar as coisas para a internet funcionar com o wifi-menu:

~~~
# pacman -S wireless_tools wpa_supplicant wpa_actiond dialog
~~~

> Por conta de esquecer de fazer isso que surgiu a dica de o que fazer caso precise voltar a utilizar o pen drive mesmo depois do sistema instalado. rs'

### Grub - Segunda parte

Pera, antes do Grub, abra o arquivo */etc/mkinitcpio.conf*. Procure por "HOOKS" e coloque antes de "filesystems" a seguinte sequência: "keymap encrypt lvm2".

Depois rode o comando:

~~~
# mkinitcpio -p linux
~~~

Agora sim, Grub:

Fazemos a instalação da segunda parte:

~~~
# grub-install /dev/sda
~~~

E edita o arquivo */etc/default/grub*, na opção *GRUB_CMDLINE_LINUX=””* para *GRUB_CMDLINE_LINUX=”cryptdevice=/dev/sda2:main”*. Depois, roda o comando:

~~~
# grub-mkconfig -o /boot/grub/grub.cfg
~~~

Acredito que está bem entendível o que essa parte fez. Mas se não, manda um comentário ai :)

### Ufa!

Pronto! Finalizamos a instalação. Agora precisamos sair do chroot e desmontar os discos:

~~~
# exit
# umount /mnt/boot
# umount /mnt/home
# umount/mnt
# reboot
~~~

Após dar o comando para reiniciar, pode tirar a mídia que utilizou para fazer a instalação e prosseguir com seu sistema tinindo.

Não custa lembrar: recomendo dar uma olhada no outro post, [a pós instalação do Arch Linux \[0\]][0].

Vlw, pessoal! Até a próxima!

## Links

~~~
[0]: {{ site.url }}{{ site.baseurl }}blog/pos-instalacao-archlinux/
[1]: http://hmarco.org/bugs/CVE-2015-8370-Grub2-authentication-bypass.html
[2]: https://www.vivaolinux.com.br/dica/LVM-Logical-Volume-Manager
[3]: https://www.vivaolinux.com.br/artigo/Entendendo-e-configurando-o-LVM-manualmente
[4]: https://www.vivaolinux.com.br/artigo/LVM-completo-e-sem-misterios
[5]: https://wiki.archlinux.org/index.php/LVM
[6]: http://www.devin.com.br/lvm/
[7]: http://www.hardware.com.br/dicas/entendendo-lvm.html
[8]: https://wiki.archlinux.org/index.php/Network_configuration_(Português)
~~~

[0]: {{ site.url }}{{ site.baseurl }}blog/pos-instalacao-archlinux/
[1]: http://hmarco.org/bugs/CVE-2015-8370-Grub2-authentication-bypass.html
[2]: https://www.vivaolinux.com.br/dica/LVM-Logical-Volume-Manager
[3]: https://www.vivaolinux.com.br/artigo/Entendendo-e-configurando-o-LVM-manualmente
[4]: https://www.vivaolinux.com.br/artigo/LVM-completo-e-sem-misterios
[5]: https://wiki.archlinux.org/index.php/LVM
[6]: http://www.devin.com.br/lvm/
[7]: http://www.hardware.com.br/dicas/entendendo-lvm.html
[8]: https://wiki.archlinux.org/index.php/Network_configuration_(Português)
