---
title: "Read The Docs のインストール"
date: 2019-07-08T17:12:49+09:00
categories:
  - Document Server
  - ドキュメントサーバー
tags:
  - Django
  - Documents
  - ドキュメント
  - Social Login
  - ソーシャルログイン
draft: false
---
ソースコード開発管理には多種多様なバージョン管理ツールが揃っているが、ドキュメントについては、同じツールを使えばいいやということか、あまり種類がない。その中でもよく使われている、[Read The Docs](https://readthedocs.org/) をインストールしてみた。

ドキュメント管理のツールなので、さぞかしドキュメントが充実しているだろう…ということはなく、やっぱり腐っているところがある。

まず第一に、プロダクションユースの設定が公開されているソース自体に含まれていない。つまり、自分で書かないといけない。この時点でまあ論外といえば論外なのだが、開発版の設定はついてくるので、[Django](https://docs.djangoproject.com/ja/2.2/) のドキュメントを眺めつつ、適宜修正。うちは、以下のようにした。バックエンドに PostgreSQL を使うように指定。ドメイン名は、仮に example.jp としておく。

```python
"""Local development settings, including local_settings, if present."""
from __future__ import absolute_import
import os

from .base import CommunityBaseSettings


class CommunityProductionSettings(CommunityBaseSettings):

    """Settings for personal production use"""

    SECRET_KEY = '(充分な長さのシークレットキー。とりあえず、ランダムな16進数で50桁もあればいいかも)'

    PRODUCTION_DOMAIN = 'www.example.jp'
    WEBSOCKET_HOST = 'www.example.jp'

    @property
    def DATABASES(self):  # noqa
        return {
            'default': {
                'ENGINE': 'django.db.backends.postgresql_psycopg2',
                'NAME': 'readthedocs',
                'USER' : 'readthedocs',
                'PASSWORD' : 'パスワード',
                'HOST' : 'localhost',
                'PORT' : '5432',
            }
        }

    # Email
    DEFAULT_FROM_EMAIL = 'no-reply@example.jp'
    SERVER_EMAIL = DEFAULT_FROM_EMAIL
    SUPPORT_EMAIL = 'support@example.jp'

    DONT_HIT_DB = False

    ACCOUNT_EMAIL_VERIFICATION = 'mandatory'
    SESSION_COOKIE_DOMAIN = 'example.jp'
    CACHE_BACKEND = 'memcached://127.0.0.1:11211'

    SLUMBER_USERNAME = 'slumberuser'
    SLUMBER_PASSWORD = 'パスワード'  # noqa: ignore dodgy check
    SLUMBER_API_HOST = 'https://www.example.jp'
    PUBLIC_API_URL = 'https://www.example.jp'

    BROKER_URL = 'redis://localhost:6379/12'
    CELERY_RESULT_BACKEND = 'redis://localhost:6379/12'
    CELERY_RESULT_SERIALIZER = 'json'
    CELERY_ALWAYS_EAGER = True
    CELERY_TASK_IGNORE_RESULT = False

    EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
    EMAIL_HOST='localhost'
    EMAIL_PORT=25
    FILE_SYNCER = 'readthedocs.builds.syncers.LocalSyncer'

    # For testing locally. Put this in your /etc/hosts:
    # 127.0.0.1 test
    # and navigate to http://test:8000
    CORS_ORIGIN_WHITELIST = (
        'example.jp',
        'www.example.jp',
    )

    ALLOWED_HOSTS = ['www.example.jp','example.jp']

    DEBUG = False
    TEMPLATE_DEBUG = False

    # Disable auto syncing elasticsearch documents in development
    ELASTICSEARCH_DSL_AUTOSYNC = True
    ELASTICSEARCH_DSL_AUTO_REFRESH = True

    # Disable password validators on development
    AUTH_PASSWORD_VALIDATORS = []

    @property
    def LOGGING(self):  # noqa - avoid pep8 N802
        logging = super().LOGGING
        logging['formatters']['default']['format'] = '[%(asctime)s] ' + self.LOG_FORMAT
        # Allow Sphinx and other tools to create loggers
        logging['disable_existing_loggers'] = False
        return logging

CommunityProductionSettings.load_settings(__name__)

if not os.environ.get('DJANGO_SETTINGS_SKIP_LOCAL', False):
    try:
        # pylint: disable=unused-wildcard-import
        from .local_settings import *  # noqa
    except ImportError:
        pass

# Allow for local settings override to trigger images name change
try:
    if DOCKER_USE_DEV_IMAGES:
        DOCKER_IMAGE_SETTINGS = {
            key.replace('readthedocs/build:', 'readthedocs/build-dev:'): settings
            for (key, settings)
            in DOCKER_IMAGE_SETTINGS.items()
        }
except NameError:
    pass
```

この内容を readthedocs/settings/production.py として保存。で、インストール開始。

- まずは、前提パッケージをインストール。

```sh
sudo apt install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

- データベースに PostgreSQL を使う場合は、libpq-dev をインストール。

```sh
sudo apt install -y libpq-dev
```

- memcached がない場合は、インストールする。

```sh
sudo apt install -y memcached
```

- redis がない場合は、インストールする。

```sh
sudo apt install -y redis-server
```

- elasticsearch がない場合は、[インストール](https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html)する。最新版の 7.x 系列で大丈夫。

- データベースとユーザーを作っておく。

```sh
$ sudo -s
# su - postgres
$ createuser -A -D -P readthedocs
$ createdb -O readthedocs readthedocs
```

- Read The Docs の実行ユーザーに su - する。

- なにやら、Python は、3.6 系統が前提みたいに、ドキュメントにあったので、pyenv で Python 3.6.8 を入れる。まずは、pyenv を git でインストール。

```sh
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

- .profile に pyenv の実行パスを追記。その上で、source .profile するか、いったんログアウトしてログインし直す。

```sh
PYENV_ROOT="$HOME/.pyenv"
export PYENV_ROOT
if [ -d "$PYENV_ROOT/bin" ] ; then
    PATH="$PYENV_ROOT/bin:$PATH"
    eval "$(pyenv init -)"
fi
```

- Apache で mod_wsgi を使う場合、共有ライブラリを使うよう指定して、Python 3.6.8 をインストールする。

```sh
env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install 3.6.8
```

- ほどなくして、インストールが終わるので、おまじないを唱える。

```sh
pyenv local 3.6.8
```

- requirements.txt を修正する。

```diff
--- requirements.txt.orig	2019-07-08 04:59:02.615529963 -0400
+++ requirements.txt	2019-07-08 04:59:10.983221608 -0400
@@ -1,2 +1,2 @@
--r requirements/pip.txt
+-r requirements/deploy.txt
 # just referencing for a natural `pip install -r requirements.txt
```

- ドキュメントにある通り、pip を実行。

```sh
pip install -r requirements.txt
```

- ドキュメント通り…ではなく、ちょこっと修正してデータベースのマイグレーションを実行。

```sh
env DJANGO_SETTINGS_MODULE=readthedocs.settings.production python manage.py migrate
```

- frontend のファイルをコンパイル

```sh
env DJANGO_SETTINGS_MODULE=readthedocs.settings.production python manage.py collectstatic
```

- 次に自分のアカウントを作る。

```sh
env DJANGO_SETTINGS_MODULE=readthedocs.settings.production python manage.py createsuperuser
```

- 同じコマンドで、SLUMBER_USERNAME に指定したユーザーも作成する。パスワードは、SLUMBER_PASSWORD に指定したものを使う。

- とりあえず、runserver して、サイトが正常に表示されることを確認する。アドレスとポートは好きなように指定する。

```sh
env DJANGO_SETTINGS_MODULE=readthedocs.settings.production python manage.py runserver 0.0.0.0:8888
```

- 確認できたら、mod_wsgi をインストールする。

```sh
pip install mod_wsgi
```

- mod_wsgi がインストールされたパスを確認して、/etc/apache2/mods-available/wsgi.load を作成する。

```apache
LoadModule wsgi_module /srv/readthedocs/.pyenv/versions/3.6.8/lib/python3.6/site-packages/mod_wsgi/server/mod_wsgi-py36.cpython-36m-x86_64-linux-gnu.so
```

- /etc/apache2/mods-available/wsgi.conf も作成する。

```apache
WSGIPythonHome /srv/readthedocs/.pyenv/versions/3.6.8
WSGIPythonPath /srv/readthedocs
```

- a2enmod して、apache を再起動。

```sh
sudo a2enmod wsgi
sudo systemctl restart apache2
```

- /etc/apache2/site-available/example.jp.conf を作成する。SSL 証明書は、Let's Encrypt とかで取得しておく。

```apache
<VirtualHost *:80>
	ServerName example.jp
	ServerAlias www.example.jp
	RewriteEngine on
	RewriteCond %{SERVER_NAME} =www.example.jp [OR]
	RewriteCond %{SERVER_NAME} =example.jp
	RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>

<IfModule mod_ssl.c>
<VirtualHost *:443>

	ServerName example.jp
	ServerAlias www.example.jp
	ServerAdmin webmaster@example.jp

	Include /etc/letsencrypt/options-ssl-apache.conf
	SSLCertificateFile /etc/letsencrypt/live/example.jp/fullchain.pem
	SSLCertificateKeyFile /etc/letsencrypt/live/example.jp/privkey.pem

	DocumentRoot /srv/readthedocs

	WSGIDaemonProcess readthedocs user=readthedocs group=readthedocs threads=5
	WSGIProcessGroup readthedocs
	WSGIApplicationGroup readthedocs
	WSGIPassAuthorization On

	WSGIScriptAlias / /srv/readthedocs/readthedocs/wsgi.py

	<Directory "/srv/readthedocs/readthedocs">
		<Files wsgi.py>
			Require all granted
		</Files>
	</Directory>
	Alias /media/ /srv/readthedocs/media/
	<Directory "/srv/readthedocs/media">
		Require all granted
	</Directory>
	Alias /static/ /srv/readthedocs/static/
	<Directory "/srv/readthedocs/static">
		Require all granted
	</Directory>

	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```

- a2ensite して、apache をリロードする。

```sh
sudo a2ensite example.jp
sudo systemctl reload apache2
```

- むろん、正常にアクセスできることを確認する。その上で、ログインを試みると、アカウント作成時に指定したアドレスへ確認メールが送信されるので、メールに記載されたアドレスを踏んで、正常にログインできるようにする。

- で、ログインする。この場合は、https://www.example.jp/login/ から。

- 正常にログインできることを確認したら、管理パネルへアクセスする。この場合、URL は、https://www.example.jp/admin/ になる。なお、ここからは**ドキュメントに書かれていない**。

- CORE > User Profile にアクセスして、SLUMBER_USERNAME で指定したユーザーの ID を確認する。

- アカウント > メールアドレス にアクセスして、SLUMBER_USERNAME のメールアドレスを追加して、「確認済み」「メイン」にチェックを入れておく。

- Read The Docs は、GitHub や、GitLab、BitBucket のリポジトリと連携して動作するよう設計されている。そこで、連携設定を管理パネルで行う。言うまでもないが、事前に各サイトで、OAuth のクライアント ID とシークレットキーを取得しておくこと。GitLab の場合、read_repository や read_user といったスコープをチェックしておかないと不正なアクセスにされてしまうので、注意。ちなみに、Callback URL は以下の通りとなる。
  - Github		https://www.example.jp/accounts/github/login/callback/
  - GitLab		https://www.example.jp/accounts/gitlab/login/callback/
  - Bitbucket	https://www.example.jp/accounts/bitbucket_oauth2/login/callback/

- 自前で GitLab のインスタンスを立ててるとか、うちは、BitBucker Server だとか、いやいや、GitHub Enterprise ですよ、うち。とか言う人は、[Django AllAuth のドキュメント](https://django-allauth.readthedocs.io/en/latest/providers.html)を確認して、設定に励んでくれたまへ。

- 管理パネルの サイト > サイト へアクセスする。すると、「example.com」が既に設定されているので、これを自分のドメイン、この場合は、「example.jp」へ変更する。

- 次に 外部アカウント > Social applications へアクセスする。

- 右上の「SOCIAL APPLICATON を追加」をクリックして、プロバイダを追加していく。その際、一番下の Sites: 欄で、**利用可能 Sites** 欄で自分のドメイン (この場合は、example.jp) を選択して、**選択された Sites** 欄に表示が移ったことを確認してから、保存ボタンをクリックすること。これを必要なプロバイダ分繰り返す。

- 追加が終われば、Read The Docs に戻って、自分のアカウント設定の「接続したサービス」から、各プロバイダへ連携が可能になっていることを確認する。

- 以上でインストールは完了である。