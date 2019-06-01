---
title: CentOS 7 の firewalld
date: 2018-01-27T08:00:14+00:00
tweet_this_url:
  - http://bit.ly/2FnF8vH
categories:
  - Server
  - Unix
  - VPS
tags:
  - CentOS
  - CentOS 7
  - Linux
  - Unix
draft: false
---
気分が乗ったので、CentOS 7 をインストールした。ファイアウォールの設定が結構手間だったので、備忘録代わりに記録しておく。

まず、定番のサービスポートを開けておく。
```
    sudo firewall-cmd --permanent --zone=public --add-service=http
    sudo firewall-cmd --permanent --zone=public --add-service=https
    sudo firewall-cmd --permanent --zone=public --add-service=pop3
    sudo firewall-cmd --permanent --zone=public --add-service=pop3s
    sudo firewall-cmd --permanent --zone=public --add-service=imap
    sudo firewall-cmd --permanent --zone=public --add-service=imaps
    sudo firewall-cmd --permanent --zone=public --add-service=smtp
    sudo firewall-cmd --permanent --zone=public --add-service=smtps
    sudo firewall-cmd --permanent --zone=public --add-service=smtp-submission
    sudo firewall-cmd --permanent --zone=public --add-service=ftp
```
自宅は固定アドレスで、かつ ipv6 も割り当てられているので、そこからは全ポートを受け付けてもらえるように開放する。
```
    sudo firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="118.243.217.235" accept'
```
```
    sudo firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv6" source address="2405:6584:7840:800::/64" accept'
```
内部通信用のインターフェースは無条件で信頼する。
```
    sudo firewall-cmd --permanent --zone=trusted --add-interface=eth1
```
設定をリロードして、おしまい。
```
    sudo firewall-cmd --reload
```
と思ったら、内部インターフェースが起動されていなかったので、NetworkManager で起動させる。
```
    sudo nmcli c m eth1 connection.autoconnect yes
    sudo nmcli c modify eth1 ipv4.addresses 192.168.207.110/24
```

<div class="tweetthis" style="text-align:left;">
  <p>
    <a onclick="javascript:pageTracker._trackPageview('/outgoing/twitter.com/intent/tweet?text=CentOS+7+%E3%81%AE+firewalld+http%3A%2F%2Fbit.ly%2F2FnF8vH');" class="tt"  href="http://twitter.com/intent/tweet?text=CentOS+7+%E3%81%AE+firewalld+http%3A%2F%2Fbit.ly%2F2FnF8vH" title="Post to Twitter"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/twitter/tt-twitter-micro4.png" alt="Post to Twitter" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld" title="Post to Digg"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/digg/tt-digg-micro4.png" alt="Post to Digg" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld" title="Post to Digg"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&t=CentOS+7+%E3%81%AE+firewalld');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&t=CentOS+7+%E3%81%AE+firewalld" title="Post to Facebook"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/facebook/tt-facebook-micro4.png" alt="Post to Facebook" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&t=CentOS+7+%E3%81%AE+firewalld');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&t=CentOS+7+%E3%81%AE+firewalld" title="Post to Facebook"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld&summary=%E6%B0%97%E5%88%86%E3%81%8C%E4%B9%97%E3%81%A3%E3%81%9F%E3%81%AE%E3%81%A7%E3%80%81CentOS+7+%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%97%E3%81%9F%E3%80%82%E3%83%95%E3%82%A1%E3%82%A4%E3%82%A2%E3%82%A6%E3%82%A9%E3%83%BC%E3%83%AB%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%81%8C%E7%B5%90%E6%A7%8B%E6%89%8B%E9%96%93%E3%81%A0%E3%81%A3%E3%81%9F%E3%81%AE%E3%81%A7%E3%80%81%E5%82%99%E5%BF%98%E9%8C%B2%E4%BB%A3%E3%82%8F%E3%82%8A%E3%81%AB%E8%A8%98%E9%8C%B2%E3%81%97%E3%81%A6%E3%81%8A%E3%81%8F%E3%80%82%0A%0A%E3%81%BE%E3%81%9A%E3%80%81%E5%AE%9A%E7%95%AA%E3%81%AE%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%83%9D%E3%83%BC%E3%83%88%E3%82%92%E9%96%8B%E3%81%91%E3%81%A6%E3%81%8A%E3%81%8F%E3%80%82%0A%0Asudo+firewall-cmd+--permanent+--zone%3Dpublic+--add-service%3Dh...&source=電脳業務日誌');" class="tt"  href="http://www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld&summary=%E6%B0%97%E5%88%86%E3%81%8C%E4%B9%97%E3%81%A3%E3%81%9F%E3%81%AE%E3%81%A7%E3%80%81CentOS+7+%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%97%E3%81%9F%E3%80%82%E3%83%95%E3%82%A1%E3%82%A4%E3%82%A2%E3%82%A6%E3%82%A9%E3%83%BC%E3%83%AB%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%81%8C%E7%B5%90%E6%A7%8B%E6%89%8B%E9%96%93%E3%81%A0%E3%81%A3%E3%81%9F%E3%81%AE%E3%81%A7%E3%80%81%E5%82%99%E5%BF%98%E9%8C%B2%E4%BB%A3%E3%82%8F%E3%82%8A%E3%81%AB%E8%A8%98%E9%8C%B2%E3%81%97%E3%81%A6%E3%81%8A%E3%81%8F%E3%80%82%0A%0A%E3%81%BE%E3%81%9A%E3%80%81%E5%AE%9A%E7%95%AA%E3%81%AE%E3%82%B5%E3%83%BC%E3%83%93%E3%82%B9%E3%83%9D%E3%83%BC%E3%83%88%E3%82%92%E9%96%8B%E3%81%91%E3%81%A6%E3%81%8A%E3%81%8F%E3%80%82%0A%0Asudo+firewall-cmd+--permanent+--zone%3Dpublic+--add-service%3Dh...&source=電脳業務日誌" title="Post to LinkedIn"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/linkedin/tt-linkedin-micro4.png" alt="Post to LinkedIn" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld" title="Post to Reddit"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/reddit/tt-reddit-micro4.png" alt="Post to Reddit" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2018/01/27/centos-7-%e3%81%ae-firewalld/&title=CentOS+7+%E3%81%AE+firewalld" title="Post to Reddit"> </a>
  </p>
</div>