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
```
sudo apt install nginx
sudo apt install php php-apcu php-bz2 php-cli php-curl php-fpm php-gettext php-imagick php-imap php-mbstring php-mdb2-driver-mysql php-mdb2-driver-pgsql php-mysql php-pgsql php-readline php-tokenizer php-xml php-xmlrpc php-zip
```

[Github](https://github.com/vanilla/vanilla/releases) からリリース版を取得。適切な位置 (仮に、/srv/vanilla とする) へ展開。

nginx の server {} ディレクティブ内で以下のように設定。
```
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
```
$Configuration['Garden']['RewriteUrls'] = true;
```

<div class="tweetthis" style="text-align:left;">
  <p>
    <a onclick="javascript:pageTracker._trackPageview('/outgoing/twitter.com/intent/tweet?text=Vanilla+Forums+http%3A%2F%2Fbit.ly%2F2J13Ace');" class="tt"  href="http://twitter.com/intent/tweet?text=Vanilla+Forums+http%3A%2F%2Fbit.ly%2F2J13Ace" title="Post to Twitter"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/twitter/tt-twitter-micro4.png" alt="Post to Twitter" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums" title="Post to Digg"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/digg/tt-digg-micro4.png" alt="Post to Digg" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums" title="Post to Digg"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2019/05/04/vanilla-forums/&t=Vanilla+Forums');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2019/05/04/vanilla-forums/&t=Vanilla+Forums" title="Post to Facebook"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/facebook/tt-facebook-micro4.png" alt="Post to Facebook" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2019/05/04/vanilla-forums/&t=Vanilla+Forums');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2019/05/04/vanilla-forums/&t=Vanilla+Forums" title="Post to Facebook"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums&summary=Debian+GNU%2FLinux+10+Buster+%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%97%E3%81%9F+VPS+%E3%81%AB%E3%80%81nginx+%E3%82%92%E5%85%A5%E3%82%8C%E3%81%A6%E3%80%81Vanilla+Forums+%E3%82%92%E7%AB%8B%E3%81%A1%E4%B8%8A%E3%81%92%E3%81%9F%E3%81%AE%E3%81%A7%E3%80%81%E3%81%9D%E3%81%AE%E3%83%A1%E3%83%A2%E3%80%82Web+%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E3%81%AB+Apache+%E3%82%92%E4%BD%BF%E3%81%86%E5%A0%B4%E5%90%88%E3%81%AF%E3%80%81.htaccess+%E3%81%AE%E3%81%B2%E3%81%AA%E5%BD%A2%E3%81%8C%E4%BA%88%E3%82%81%E4%BB%95%E8%BE%BC%E3%81%BE%E3%82%8C%E3%81%A6%E3%82%8B%E3%81%AE%E3%81%A7%E3%80%81%E6%B3%A8%E6%84%8F%E7%82%B9%E3%81%AF%E3%81%AA%E3%81%84%E3%80%82%0D%0A%0D%0A%E3%81%BE%E3%81%9A%E3%81%AF...&source=電脳業務日誌');" class="tt"  href="http://www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums&summary=Debian+GNU%2FLinux+10+Buster+%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%97%E3%81%9F+VPS+%E3%81%AB%E3%80%81nginx+%E3%82%92%E5%85%A5%E3%82%8C%E3%81%A6%E3%80%81Vanilla+Forums+%E3%82%92%E7%AB%8B%E3%81%A1%E4%B8%8A%E3%81%92%E3%81%9F%E3%81%AE%E3%81%A7%E3%80%81%E3%81%9D%E3%81%AE%E3%83%A1%E3%83%A2%E3%80%82Web+%E3%82%B5%E3%83%BC%E3%83%90%E3%83%BC%E3%81%AB+Apache+%E3%82%92%E4%BD%BF%E3%81%86%E5%A0%B4%E5%90%88%E3%81%AF%E3%80%81.htaccess+%E3%81%AE%E3%81%B2%E3%81%AA%E5%BD%A2%E3%81%8C%E4%BA%88%E3%82%81%E4%BB%95%E8%BE%BC%E3%81%BE%E3%82%8C%E3%81%A6%E3%82%8B%E3%81%AE%E3%81%A7%E3%80%81%E6%B3%A8%E6%84%8F%E7%82%B9%E3%81%AF%E3%81%AA%E3%81%84%E3%80%82%0D%0A%0D%0A%E3%81%BE%E3%81%9A%E3%81%AF...&source=電脳業務日誌" title="Post to LinkedIn"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/linkedin/tt-linkedin-micro4.png" alt="Post to LinkedIn" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums" title="Post to Reddit"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/reddit/tt-reddit-micro4.png" alt="Post to Reddit" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2019/05/04/vanilla-forums/&title=Vanilla+Forums" title="Post to Reddit"> </a>
  </p>
</div>