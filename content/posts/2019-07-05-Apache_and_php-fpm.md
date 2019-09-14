---
title: "Apache で php-fpm を使う"
date: 2019-07-05T05:12:38+09:00
categories:
  - Server
  - Web
  - Apache
  - PHP
tags:
  - Apache
  - PHP
  - php-fpm
draft: false
---

やっぱり、Apache でも http2 を有効にしたい！ということで、慣れ親しんだ、php_module からおさらばして、php-fpm で構成し直した。Debian & php 7.3 での例を示す。

まず、php-fpm をインストール。まあ、php_module を削除すれば、勝手に php-fpm が入るんですが。ダウンタイムを極力避けるなら、この手順で。

```sh
sudo apt install php-fpm
```

次に proxy_fcgi を有効にする。
```sh
sudo a2enmod proxy_fcgi
```

そうしたら、php_module を削除する。
```sh
sudo apt purge libapache2-mod-php libapache2-mod-php7.3
```

prefork モジュールが読み込まれているのをやめて、event モジュールに差し替える。ついでに、http2 モジュールを有効にする。

```sh
sudo a2dismod mpm_prefork
sudo a2enmod mpm_event http2
```

最後に、Apache の php-fpm 設定を有効にする。

```sh
sudo a2enconf php7.3-fpm
```

あとは、Apache を再起動するだけ。
```sh
sudo systemctl restart apache2
```

うむ。簡単だった。