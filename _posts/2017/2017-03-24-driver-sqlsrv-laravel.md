---
layout: post
title:	"Driver SQLSrv com Laravel em Linux"
date:	2017-03-24 01:00:00
categories:
    - tips
tags:
    - laravel
    - linux
    - php
    - sqlserver
    - webdev
---

Fala, pessoal! Tudo certo?

Bem, veja só essa questão: entrei em um projeto que tem envolvimento com SQL Server e é para ser feito com Laravel. Acontece que uso Linux, então existe o driver `dblib` que seria uma alternativa para o `sqlsrv`. Instalei-o, tudo certo. A questão é que o Laravel não suporta esse driver, mas ainda assim, conseguia ao menos conectar no banco.

O problema é quando ia fazer algo como `composer install` ou um simples `php artisan --help`, ele dava o seguinte erro:

~~~
SQLSTATE[IM001]: Driver does not support this function: driver does not support getting attributes
~~~

E colocando a opção `-vvv`:

~~~
> post-install-cmd: Illuminate\Foundation\ComposerScripts::postInstall
> post-install-cmd: php artisan optimize
Executing command (CWD): php artisan optimize


  [PDOException]
    SQLSTATE[IM001]: Driver does not support this function: driver does not support getting attributes


    Script php artisan optimize handling the post-install-cmd event returned with error code 1
~~~

Pesquisei em vários locais para como resolver isso e não encontrei nada, então fiquei mais "WTF?" ainda, e fui atrás. Até que consegui fazer SQLSrv rodar no Linux e então fui instalando as demais dependências.

O script básico que fiz segue abaixo:

~~~
#!/bin/bash

# update package list
apt-get update

# install curl
apt-get install -y curl

# install git
apt-get install -y git

# install apache
apt-get install -y apache2

# install php
apt-get -y install php7.0 mcrypt php7.0-mcrypt php-mbstring php-pear php7.0-dev php7.0-xml
apt-get install -y libapache2-mod-php7.0

# install pre requisites
apt-get update
apt-get install -y apt-transport-https
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
apt-get update
ACCEPT_EULA=Y apt-get install -y msodbcsql mssql-tools
apt-get install -y unixodbc-utf16
apt-get install -y unixodbc-dev-utf16

# install driver sqlsrv
pecl install sqlsrv
# You should add "extension=sqlsrv.so" to php.ini
echo "extension=sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
pecl install pdo_sqlsrv
# You should add "extension=pdo_sqlsrv.so" to php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.0/apache2/php.ini

# load driver sqlsrv
echo "extension=/usr/lib/php/20151012/sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
echo "extension=/usr/lib/php/20151012/pdo_sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
echo "extension=/usr/lib/php/20151012/sqlsrv.so" >> /etc/php/7.0/cli/php.ini
echo "extension=/usr/lib/php/20151012/pdo_sqlsrv.so" >> /etc/php/7.0/cli/php.ini

# restart apache
service apache2 restart

# test with phpinfo
echo "<?php phpinfo();" > /var/www/html/info.php

# install composer
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
mv composer.phar /usr/local/bin/composer

# ODBC Driver
ACCEPT_EULA=Y apt-get install -y msodbcsql
apt-get install -y mssql-tools
apt-get install -y unixodbc-dev
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc">"
~~~

Para tentar minimizar as chances de dar merda, criei uma imagem docker para isso: [gjuniioor/php-sqlsrv \[0\]][0].

Para rodar, basta executar algo como:

~~~
$ docker run -d -p 80:80 -v projeto/laravel:/var/www/html gjuniioor/php-sqlsrv:7.0
~~~

Então dentro do container fazer o padrão para rodar o projeto, instalar as dependências, rodar as migrations, enfim.

Bem, é isso. Busquei mais ainda vir aqui postar isso para que quem procurar por algo assim agora possa encontrar com uma solução.

Até a vista!!

## Links

~~~
[0]: https://hub.docker.com/r/gjuniioor/php-sqlsrv
~~~

[0]: https://hub.docker.com/r/gjuniioor/php-sqlsrv
