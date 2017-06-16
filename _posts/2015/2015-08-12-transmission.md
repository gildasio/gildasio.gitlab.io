---
layout: post
title:  "Transmission - Gerencie seus torrents em CLI"
date:   2015-08-12 11:16:48
categories:
    - tips
tags:
    - linux
    - terminal
    - cli lindo!
---

> **OBS:** Olha só galera, dando continuidade ao estilo de post falando sobre ferramentas em CLI. Parece que vai dar certo... (a partir de um artigo já é série haha)

Aqui irei mostrar como utilizar o Transmission, claro, pelo terminal ou console.

## Definição

Transmission é um cliente Bit-torrent... Torrent pode ser rapidamente definido como um protocolo para transferência de arquivos. É altamente utilizado... Dizem as más línguas que ele é muito usado para transporte de coisas ilegais e pirataria, mas estou por fora desses dados. :P

<!--more-->


De qualquer modo, vou mostrar como gerenciar os torrents que estejam em download por ele.

Ah, aqui tem um artigo sobre comparação entre softwares da área: https://en.wikipedia.org/wiki/Comparison_of_BitTorrent_clients

## Instalação

Será necessário instalar dois pacotes para isso: `transmission-cli` e `transmission-remote-cli`. O primeiro trás três programas bem importantes: `transmission-daemon`, `transmission-remote` e `transmission-web`. Explico o que é cada um:

- `transmission-daemon`: Daemon que faz com que o serviço de cliente fique funcionando depois que habilitar.
- `transmission-remote`: Uma ferramenta por linha de comando para gerenciar os torrents
- `transmission-web`: Uma interface web (na porta 9091) para gerenciar os torrents
- `transmission-remote-cli`: Ferramenta CLI para gerenciar os torrents (meu favorito)

Portanto, para quem utiliza o Arch basta rodar:

~~~
# pacman -S transmission-cli transmission-remote-cli
~~~

Para quem utiliza outros sistemas, deve saber utilizar o gerenciador de pacotes que roda por ai. Caso não, comenta que a gente se une na causa.

## Daemon

Vou primeiramente tratar sobre o *Daemon* do serviço. Para termos nossa máquina baixando os torrents basta iniciar esse daemon. Para adicionar, remover, pausar e demais ações aí sim vamos precisar dos outros... Logo, o *daemon* é o mais importante...

Para iniciar:

~~~
$ transmission-daemon
~~~

E para finalizar:

~~~
$ killall transmission-daemon
~~~

Uma alternativa para isso seria usar `transmission-remote --exit`, mas acho a primeira forma melhor.

Para habilitar para já rodar quando ligar o computador, pesquise sobre scripts de inicialização, afinal, esse não é o intuito do artigo.

## Configuração de usuário e senha

O arquivo de configuração do Transmission está em `~/.config/transmission-daemon/settings.json` e já tem muita coisa lá, basta habilitar ou não.

No caso da autenticação, procure pela linha que contenha `rpc-authentication-required` e mude para `true`. Recomendo que mude também ao menos a senha em `rpc-password`. Pode ficar a vontade para mudar o usuário também, é bem intuitivo isso.

## Abrindo para acessar de outros computadores

Por padrão, é configurado para o acesso ser apenas pelo próprio computador. Se fosse assim, para mim, perderia o valor da interface web. :)

Mas eu gosto de utilizar as vezes pelo celular... Então, podemos abrir o acesso para demais computadores da rede. Apenas edite o arquivo de configuração (que você já deve saber onde é, se não sabe, está lendo esse post de forma errada).

No parâmetro `rpc-whitelist` coloque um coringa, `*`. Pronto! Ah, a interface web para celular é bacana... Bem mobile friendly.

## Diretório de Download

Acho bom configurar isso para ficar organizado da melhor forma que quiser... Simplesmente, altere o valor em `download-dir`. 

Para completar essa dica, gostaria de falar sobre o diretório para downloads incompletos... É a opção `incomplete-dir`. Eu deixo basicamente da seguinte forma: `download/finish` e `download/incomplete` para que possa ficar bem organizado.

## Monitorando um diretório

Tem uma opção bacana que é permitido de configurar. É a de o transmission ficar monitorando um determinado diretório e quando surgir um arquivo .torrent ele já começar adicionar e começar o download. Isso é bacana pois basta você fazer o download do .torrent e pronto, seja feliz. 

Um outro uso que curto demais é direcionar para um diretório que faz parte da sincronia de algum desses programas, como Dropbox, Mega... Pois ai de qualquer lugar do mundo você salva o arquivo nele, e enquanto seu computador sincroniza, o transmission já olha o arquivo e pronto.

A opção que configura isso são as seguintes:

~~~
"watch-dir": "~/directory/to/watch",
"watch-dir-enable": true
~~~

Mas acontece de em certos momentos isso não funcionar e ainda não encontrei o motivo. Você pode rodar o daemon da seguinte forma, e isso funciona rsrs:

~~~
$ transmission-daemon -c ~/directory/to/watch
~~~

Pode-se criar um alias para executar de forma mais simples.

## Outras configurações

Você pode mexer em todos os parâmetros que tem no arquivo. Fique a vontade para isso! E pode também acrescentar mais! Dê uma lida nesse na [documentação](https://trac.transmissionbt.com/wiki/EditConfigFiles#Options) e pronto.

## Remote CLI

Agora vamos chegar numa das partes mais interessantes: a de gerenciar os torrents pelo cliente CLI.

A sintaxe básica para entrar é: `transmission-remote-cli -c usuario:senha@servidor:porta`...

Em caso de não ter alterado a porta e nem ter habilitado a autenticação, basta omitir esses dados.

Já dentro da aplicação, vamos ver alguns comandos:

#### Adicionar arquivo

Aperte `a` e irá aparecer uma caixa de diálogo. Se for inserir um arquivo, basta colocar o link para ele. Se for inserir a partir de um link magnético, apague o `~` que já tem (é uma forma de ajudar para quando formos colocar o arquivo) e cole o link.

#### Remover arquivo

Para remover item do download você digita `r`. 

A opção `R` vai remover também os arquivos baixados até então. Muito útil quando quer cancelar downloads que não devia ter começado. Uma dor de cabeça quando quer remover os que já terminaram.

#### Pausa e Continuação

Para isso, usa-se a opção `p`. Ele vai pausar ou continuar o download do item selecionado.

Se quiser pausar/continuar o download de todos os itens, basta usar em maiúsculo, `P`.

#### Fechar o cliente

Se quiser sair do programa, basta digitar `q`.

#### Buscando torrents

Você pode estar baixando várias coisas e quer localizar um com mais facilidade. Então, pressione `/` e pode digitar o título para procurar.

#### Ordenar a exibição

Para melhorar a navegação, você pode ordenar a exibição dos itens. Digite `s` e terá um menu para escolher por onde ordenar.

#### Informações Sobre o Item

Você pode querer ver mais informações sobre o download, como outros *Peers*. Então, pressione `Enter` e continue navegando com as setas. Para sair basta pressionar `Esc`.

## Conclusão

Bem galera, é isso... Só um adendo: cuidado com o que vão baixar.

No mais, se divirtam... E nada de consumir tanta memória RAM haha Se tem ótima opção CLI, para quer GUI? De qualquer modo, fica a gosto do freguês... Até mais ver.
