---
title: "Formspree"
date: 2019-08-12T13:29:10+09:00
categories:
  - メール
  - mail
  - Web
  - サーバー
  - server
tags:
  - Formspree
  - Mail Form
  - メールフォーム
draft: false
---

例によって例のごとく、ドキュメントが未整備なオープンソースアプリをインストールしたので、そのメモ。

[Formspree](https://github.com/formspree/formspree) は、静的サイトなどにメールフォームを設置するためのサーバーアプリケーションである。設置が面倒な方は、[ホスティングサービス](https://formspree.io/)もあるので、そちらを利用された方がよいかと。

- まず、Python をインストールする。Python は、個人的に pyenv を使うので、そのように。
	```sh
	git clone https://github.com/pyenv/pyenv.git ~/.pyenv
	```

- .profile を編集して、以下を追記。
	```sh
	PYENV_ROOT="$HOME/.pyenv"
	export PYENV_ROOT
	if [ -d "$PYENV_ROOT/bin" ] ; then
	    PATH="$PYENV_ROOT/bin:$PATH"
	    eval "$(pyenv init -)"
	fi
	```
- 前提ファイルをインストール
	```sh
	sudo apt install build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev libmariadb-dev-compat libpq-dev
	```
- Node.js もインストールしておく。
	```sh
	curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
	sudo apt install -y nodejs
	```
- Python をインストール。その後、pipenv をインストール。
	```sh
	pyenv install 3.7.4
	pyenv local 3.7.4
	pip install pipenv
	```

- Formspree のリポジトリをコピーする。
	```sh
	git clone https://github.com/formspree/formspree
	cd formspree
	```

- Pipfile を編集して、Python 3.7 に対応させる。
	```diff
	--- Pipfile.orig	2019-08-12 13:42:23.725887560 +0900
	+++ Pipfile	2019-08-12 01:52:39.381882527 +0900
	@@ -10,7 +10,7 @@
	 pylint = "*"

	 [requires]
	-python_version = "3.6"
	+python_version = "3.7"

	 [packages]
	 celery = "==4.2.0"
	```

- 依存パッケージをインストール。
	```sh
	pipenv install
	```

- フロントエンドパッケージをインストール
	```sh
	npm install
	make
	make prod
	```
	
- gunicorn 用の設定ファイルを作成する。例えば、以下の通り。
	```python
	import multiprocessing

	bind     = '127.0.0.1:8888'
	workers  = multiprocessing.cpu_count() * 2 + 1
	chdir    = '/srv/formspree/formspree'
	logfile  = '/srv/formspree/logs/access.log'
	loglevel = 'info'
	```
- .env 設定ファイルを作成する。たとえば、以下の通り。
	```sh
	API_ROOT='https://example.com'
	CONTACT_EMAIL='admin@example.com'
	DATABASE_URL='postgresql://formspree:password@127.0.0.1:5432/formspree'
	DEBUG='True'
	DEFAULT_SENDER='no-reply@example.com'
	LOG_LEVEL='info'
	MONTHLY_SUBMISSIONS_LIMIT='1000'
	NONCE_SECRET='ランダムな文字列'
	HASHIDS_SALT='ランダムな文字列'
	REDISTOGO_URL='127.0.0.1:6379'
	SECRET_KEY='ランダムな文字列'
	SENDGRID_PASSWORD='SendGrid ログインパスワード'
	SENDGRID_USERNAME='SendGrid ログインユーザー名'
	SERVICE_NAME='Mail Form'
	SERVICE_URL='https://example.com'
	RECAPTCHA_SECRET='xxx'
	RECAPTCHA_KEY='xxx'
	```

- .env ファイルの DATABASE_URL でアクセスできるデータベースを作成し、以下のコマンドでテーブルを作成する。
	```sh
	env FLASK_APP=formspree/manage.py pipenv run flask db upgrade
	```
	
- gunicorn 起動用の systemd ファイルを /lib/systemd/system/formspree.service などとして作成する。
	```systemd
	[Unit]
	Description=Formspree Gunicorn
	After=network.target

	[Service]
	Type=simple
	User=formspree
	Group=formspree
	Environment=FLASK_APP=formspree/manage.py
	WorkingDirectory=/srv/formspree/formspree
	ExecStart=/srv/formspree/.pyenv/shims/pipenv run gunicorn \
		formspree:app \
		--config /srv/formspree/config.py
	Restart=on-abort

	[Install]
	WantedBy=multi-user.target
	```

- 起動する。
	```sh
	systemctl enable formspree
	systemctl start formspree
	```
	
- エラーがなければ、Apache を設定する。
	```apache
	<VirtualHost *:80>
		ServerName example.com
		ServerAlias www.example.com
		RewriteEngine on
		RewriteCond %{SERVER_NAME} =example.com [OR]
		RewriteCond %{SERVER_NAME} =www.example.com
		RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
	</VirtualHost>

	<IfModule mod_ssl.c>
	<VirtualHost *:443>

		ServerName example.com
		ServerAlias www.example.com
		ServerAdmin webmaster@example.com

		Include /etc/letsencrypt/options-ssl-apache.conf
		SSLCertificateFile /etc/letsencrypt/live/example.com/fullchain.pem
		SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem

		RewriteEngine On
		RewriteCond %{HTTP_HOST} ^www\.(.*)$ [NC]
		RewriteRule ^(.*)$ http://%1/$1 [R=301,L]

		Alias /static/ /srv/formspree/formspree/formspree/static/
		<Directory "/srv/formspree/formspree/formspree/static">
			Require all granted
		</Directory>

		RequestHeader set X-Forwarded-Proto "https"
		ProxyPreserveHost On
		ProxyPass /static !
		ProxyPass / http://127.0.0.1:8888/
		ProxyPassReverse / http://127.0.0.1:8888/

		ErrorLog ${APACHE_LOG_DIR}/error.log
		CustomLog ${APACHE_LOG_DIR}/access.log combined

	</VirtualHost>
	</IfModule>

	# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
	```
	
- 登録画面にアクセスして、ユーザー登録した後で、データベースを直接書き換えて、自分を Gold ユーザーにしておくことをお忘れなく。でないと、全機能が使えません。
	```sql
	update users set plan = 'v1_platinum';
	```