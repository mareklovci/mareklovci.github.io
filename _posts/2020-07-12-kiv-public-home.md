---
title: "Nasazení webové aplikace na servery KIV"
published: true
---

V rámci projektu na předmět KIV/ASWI jsem potřeboval vystavit webovou aplikaci.
Fakulta pro požadavky studentů vytvořila prostor právě pro takové účely.
Rozcestník a seznam podporovaných technologií je dostupný na adrese http://students.kiv.zcu.cz/.

Při nasazování aplikace (PHP + Laravel) jsem postupoval následujícím způsobem.

## Prerekvizity

Prerekvizitou je, že projekt generuje html soubory do složky `public_html`, generovat je do složky `public` nestačí.
V mém případě pro Laravel 7.x jsem postupoval dle tohoto návodu https://medium.com/@pixelvars/laravel-change-public-html-to-public-html-the-right-way-496431aed94.

## Přístup na server

Pro přístup na server je nutné použít SSH.

```sh
ssh <orion-login>@students.kiv.zcu.cz
```

Po vyzvání je nutné zadat orion heslo náležící k účtu.
Po správném zadání je uživatel přihlášen na server.

## Zkopírování projektu

Projekt, který je potřeba vystavit je hostován na službě GitLab.

```sh
git clone https://gitlab.kiv.zcu.cz/aswi/aswi-2020/aswi2020merlot.git
```

Následně přesuneme soubory z právě vytvořené složky do složky `public-kiv`.

```sh
mv -v aswi2020merlot/* public-kiv/
```

Odstraníme prázdnou složku.

```sh
rm -rf aswi2020merlot/
```

## Instalace projektu

Následně budu vycházet z postupu uvedeného v článku [How to Setup a Laravel Project You Cloned from Github.com](https://devmarketer.io/learn/setup-laravel-project-cloned-github-com/).

### Instalace `composer`

Na serveru není nainstalován composer, který je potřeba pro instalaci Laravelu.
Vycházím z příkazů uvedených na stránce https://getcomposer.org/download/.

```sh
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

php -r "if (hash_file('sha384', 'composer-setup.php') === 'e5325b19b381bfd88ce90a5ddb7823406b2a38cff6bb704b0acc289a09c8128d4a8ce2bbafcd1fcbdc38666422fe2806') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

php composer-setup.php

php -r "unlink('composer-setup.php');"
```

### Instalace `composer` závislostí

Obvykle by se použil příkaz `composer install`, my však musíme použít jeho modifikovanou verzi.

```sh
php composer.phar install
```

V konfiguračním souboru jsme definovali připojení do *sqlite* databáze, která však není dosud vytvořená.

```sh
cd database
touch database.sqlite
cd ..
```

Nyní je třeba vygenerovat šifrovací klíč.

```sh
php artisan key:generate
```

Zmigrujeme databázi.

```sh
php artisan migrate
```

Naplníme databázi daty.

```sh
php artisan db:seed
```

## Závěr

Aplikace by měla být dostupná na adrese `http://students.kiv.zcu.cz/~lovcim/`.
Jeden problém je ten, že se mi nedaří přinutit Laravel aby generoval html do složky `public_html` místo původní složky `public`.
Druhý problém je ten, že z nějakého důvodu se nedokončí migrace a musí být tedy ručně ukončena.
Prezentace stále nefunguje.

### V případě neexistence konfiguračního souboru

Všechny soubory ve složce zobrazíme pomocí příkazu `ls -a`.
V případě, že chybí soubor `.env`, tak ho musíme vytvořit ručně.

```sh
touch .env
```

Zkopírovat obsah původního souboru do nově vytvořeného pomocí editoru *vim* `vim .env`.

```
APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:eko5rHfrbQCv2hHl8aT4FnKC+EjC/JJG6mKqbzmZFhM=
APP_DEBUG=false
APP_URL=http://students.kiv.zcu.cz/~lovcim/

LOG_CHANNEL=stack

DB_CONNECTION=sqlite

BROADCAST_DRIVER=log
CACHE_DRIVER=file
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=kaplicky@students.kiv.zcu.cz
MAIL_FROM_NAME="${APP_NAME}"

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_APP_CLUSTER=mt1

MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
MIX_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"
```

### Pomůcky

*Odstranění souborů ve složce se zachováním složky samotné*

```sh
rm -rfv public-kiv/*
```
