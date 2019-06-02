---
title: Debian Squeeze に Xen 4.1 を入れる
date: 2012-03-26T01:31:58+00:00
tweet_this_url:
  - http://bit.ly/H18D6N
categories:
  - Dedicated Server
  - Server
tags:
  - Server
  - Virtual Host
  - Virtual Private Server
  - Xen
draft: false
---
XenServer 6.0 の基盤になってたり、他のディストリがこぞって採用してるのが、Xen 4.1 なのですが、時期の関係で、Squeeze には、4.0 が収録されています。何か中途半端。sid にはパッケージがありますので、そっからソースを取ってきて（さすがにバイナリは持ってきても動かないので）、ビルドする方法を見つけましたので、備忘録がてら。

元ネタはこちら → [Xen 4.1 from source with Debian Squeeze 2.6.32-5-xen-amd64 dom0 (test)](http://www.gossamer-threads.com/lists/xen/users/203650)

まずは、source.list に１行追加。
```list
deb-src http://ftp.jp.debian.org/debian/ sid main
```

squeeze や wheezy の行があれば、コメントアウトしておきます。 

で、おもむろに、ビルド…する前に、パッケージをひとつ追加しておきます。ないとコンパイルがエラーになるので。
```bash
apt-get install ipxe-qemu
```

PXEブートに使うファームのQEMU用ROMイメージなんですが、なぜか Xen をインストールしても、build-dep しても入りません。 

まずはビルド環境を整えます。
```bash
apt-get update
apt-get build-dep xen
apt-get build-dep xen-utils-common
```

Xen のソースと Debian パッチの取り寄せ、ビルドも apt-get で済むのが便利なところ。
```bash
cd /usr/src/
apt-get source xen -b
apt-get source xen-utils-common -b
```

エラーがなければパッケージができているので、dpkg でインストールすればおしまい。
```bash
dpkg -i *xen*deb
```

<div class="tweetthis" style="text-align:left;">
  <p>
    <a onclick="javascript:pageTracker._trackPageview('/outgoing/twitter.com/intent/tweet?text=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B+http%3A%2F%2Fbit.ly%2FH18D6N');" class="tt"  href="http://twitter.com/intent/tweet?text=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B+http%3A%2F%2Fbit.ly%2FH18D6N" title="Post to Twitter"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/twitter/tt-twitter-micro4.png" alt="Post to Twitter" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B" title="Post to Digg"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/digg/tt-digg-micro4.png" alt="Post to Digg" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B" title="Post to Digg"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&t=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&t=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B" title="Post to Facebook"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/facebook/tt-facebook-micro4.png" alt="Post to Facebook" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&t=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&t=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B" title="Post to Facebook"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B&summary=XenServer+6.0+%E3%81%AE%E5%9F%BA%E7%9B%A4%E3%81%AB%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%9F%E3%82%8A%E3%80%81%E4%BB%96%E3%81%AE%E3%83%87%E3%82%A3%E3%82%B9%E3%83%88%E3%83%AA%E3%81%8C%E3%81%93%E3%81%9E%E3%81%A3%E3%81%A6%E6%8E%A1%E7%94%A8%E3%81%97%E3%81%A6%E3%82%8B%E3%81%AE%E3%81%8C%E3%80%81Xen+4.1+%E3%81%AA%E3%81%AE%E3%81%A7%E3%81%99%E3%81%8C%E3%80%81%E6%99%82%E6%9C%9F%E3%81%AE%E9%96%A2%E4%BF%82%E3%81%A7%E3%80%81Squeeze+%E3%81%AB%E3%81%AF%E3%80%814.0+%E3%81%8C%E5%8F%8E%E9%8C%B2%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99%E3%80%82%E4%BD%95%E3%81%8B%E4%B8%AD%E9%80%94%E5%8D%8A%E7%AB%AF%E3%80%82sid+%E3%81%AB%E3%81%AF%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%8C%E3%81%82%E3%82%8A%E3%81%BE%E3%81%99%E3%81%AE%E3%81%A7%E3%80%81%E3%81%9D%E3%81%A3%E3%81%8B%E3%82%89%E3%82%BD%E3%83%BC%E3%82%B9%E3%82%92%E5%8F%96%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%A6%EF%BC%88%E3%81%95%E3%81%99%E3%81%8C%E3%81%AB%E3%83%90%E3%82%A4%E3%83%8A%E3%83%AA%E3%81%AF%E6%8C%81%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%A6%E3%82%82%E5%8B%95%E3%81%8B...&source=電脳業務日誌');" class="tt"  href="http://www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B&summary=XenServer+6.0+%E3%81%AE%E5%9F%BA%E7%9B%A4%E3%81%AB%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%9F%E3%82%8A%E3%80%81%E4%BB%96%E3%81%AE%E3%83%87%E3%82%A3%E3%82%B9%E3%83%88%E3%83%AA%E3%81%8C%E3%81%93%E3%81%9E%E3%81%A3%E3%81%A6%E6%8E%A1%E7%94%A8%E3%81%97%E3%81%A6%E3%82%8B%E3%81%AE%E3%81%8C%E3%80%81Xen+4.1+%E3%81%AA%E3%81%AE%E3%81%A7%E3%81%99%E3%81%8C%E3%80%81%E6%99%82%E6%9C%9F%E3%81%AE%E9%96%A2%E4%BF%82%E3%81%A7%E3%80%81Squeeze+%E3%81%AB%E3%81%AF%E3%80%814.0+%E3%81%8C%E5%8F%8E%E9%8C%B2%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%81%BE%E3%81%99%E3%80%82%E4%BD%95%E3%81%8B%E4%B8%AD%E9%80%94%E5%8D%8A%E7%AB%AF%E3%80%82sid+%E3%81%AB%E3%81%AF%E3%83%91%E3%83%83%E3%82%B1%E3%83%BC%E3%82%B8%E3%81%8C%E3%81%82%E3%82%8A%E3%81%BE%E3%81%99%E3%81%AE%E3%81%A7%E3%80%81%E3%81%9D%E3%81%A3%E3%81%8B%E3%82%89%E3%82%BD%E3%83%BC%E3%82%B9%E3%82%92%E5%8F%96%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%A6%EF%BC%88%E3%81%95%E3%81%99%E3%81%8C%E3%81%AB%E3%83%90%E3%82%A4%E3%83%8A%E3%83%AA%E3%81%AF%E6%8C%81%E3%81%A3%E3%81%A6%E3%81%8D%E3%81%A6%E3%82%82%E5%8B%95%E3%81%8B...&source=電脳業務日誌" title="Post to LinkedIn"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/linkedin/tt-linkedin-micro4.png" alt="Post to LinkedIn" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B" title="Post to Reddit"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/reddit/tt-reddit-micro4.png" alt="Post to Reddit" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2012/03/26/debian-squeeze-%e3%81%ab-xen-4-1-%e3%82%92%e5%85%a5%e3%82%8c%e3%82%8b/&title=Debian+Squeeze+%E3%81%AB+Xen+4.1+%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B" title="Post to Reddit"> </a>
  </p>
</div>