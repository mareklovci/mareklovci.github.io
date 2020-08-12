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

V konfiguračním souboru jsme definovali připojení do *sqlite* databáze, která však není dosud vytvořená.

```sh
cd database
touch database.sqlite
cd ..
```

Obvykle by se použil příkaz `composer install`, my však musíme použít jeho modifikovanou verzi.

```sh
php composer.phar install
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
Jeden problém je ten, aplikace hlásí 500 error.
Druhý problém je ten, že z nějakého důvodu se nedokončí migrace a musí být tedy ručně ukončena.

### Pomůcky

*Odstranění souborů ve složce se zachováním složky samotné*

```sh
rm -rfv public-kiv/*
```

*Vytvoření nového souboru*

```sh
touch .env
```

*Zobrazení všech (i skrytých) souborů ve složce*

```sh
Všechny soubory ve složce zobrazíme pomocí příkazu `ls -a`.
```
