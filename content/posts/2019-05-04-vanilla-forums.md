---
title: Vanilla Forums
date: 2019-05-04T10:36:17+00:00
tweet_this_url:
  - http://bit.ly/2J13Ace
categories:
  - Server
  - Software
  - Unix
  - VPS
  - Web
tags:
  - Debian
  - Ngnix
  - PHP
  - Vanilla Forums
draft: false
---
Debian GNU/Linux 10 Buster をインストールした VPS に、nginx を入れて、[Vanilla Forums](https://github.com/vanilla/vanilla) を立ち上げたので、そのメモ。Web サーバーに Apache を使う場合は、.htaccess のひな形が予め仕込まれてるので、注意点はない。

まずは、nginx と php をインストール
```bash
sudo apt install nginx
sudo apt install php php-apcu php-bz2 php-cli php-curl php-fpm php-gettext php-imagick php-imap php-mbstring php-mdb2-driver-mysql php-mdb2-driver-pgsql php-mysql php-pgsql php-readline php-tokenizer php-xml php-xmlrpc php-zip
```
[Github](https://github.com/vanilla/vanilla/releases) からリリース版を取得。適切な位置 (仮に、/srv/vanilla とする) へ展開。

nginx の server {} ディレクティブ内で以下のように設定。
```nginx
root /srv/vanilla;

# Add index.php to the list if you are using PHP
index index.php;

# Block some folders as an extra hardening measure.
location ~* "/\.git" { deny all; return 403; }
location ~* "^/build/" { deny all; return 403; }
location ~* "^/cache/" { deny all; return 403; }
location ~* "^/cgi-bin/" { deny all; return 403; }
location ~* "^/uploads/import/" { deny all; return 403; }
location ~* "^/conf/" { deny all; return 403; }
location ~* "^/tests/" { deny all; return 403; }
location ~* "^/vendor/" { deny all; return 403; }
location ^~ "/favicon.ico" { access_log off; log_not_found off; return 404; }

# This handles all the main requests thru index.php.
location ~ \.php$ {
	# send to fastcgi
	include fastcgi.conf;
	fastcgi_index index.php;
	fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
	fastcgi_pass unix:/run/php/php7.3-fpm.sock;
}

# Default path handling
location / {
	try_files $uri @vanilla;
}

location @vanilla {
	fastcgi_param X_VANILLA 1;
	rewrite ^/(.+)$ /index.php?p=$1 last;
}
```

/srv/vanilla/conf/config.php に以下の設定を追加
```php
$Configuration['Garden']['RewriteUrls'] = true;
```
