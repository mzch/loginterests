---
title: DragonFly BSD の IPv6 設定問題
date: 2018-01-21T21:47:10+00:00
tweet_this_url:
  - http://bit.ly/2G0ljf3
categories:
  - Management
  - Server
  - Unix
tags:
  - DragonFly
  - DragonFly BSD
  - Unix
draft: false
---
なぜか、/etc/rc.conf に以下の設定をしても反映されない。

```
ipv6_enable="YES"
ipv6_network_interfaces="vtnet0"
ipv6_ifconfig_vtnet0="inet6 2001:470:d:461::7:1 prefixlen 64"
ipv6_defaultrouter="2001:470:d:461::1"
```
仕方ないので、/etc/rc.local にコマンドを直書きしてごまかした。
```
#! /bin/sh
ifconfig vtnet0 inet6 2001:470:d:461::7:1 prefixlen 64 alias&lt;br />
route add -inet6 default 2001:470:d:461::1&lt;br />
```

~~解決法をご存じの方がいらしたら、ぜひコメントをお願いしたい。~~

追記。
  
メーリングリストで質問したら、ipv6\_ifconfig\_vtnet0 の設定がよくないと指摘された。
```
-ipv6_ifconfig_vtnet0="inet6 2001:470:d:461::7:1 prefixlen 64"
+ipv6_ifconfig_vtnet0="2001:470:d:461::7:1"
```
と、アドレスだけ指定するのが、DragonFly での作法とか。指摘してくれた、Aaron に感謝。

<div class="tweetthis" style="text-align:left;">
  <p>
    <a onclick="javascript:pageTracker._trackPageview('/outgoing/twitter.com/intent/tweet?text=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C+http%3A%2F%2Fbit.ly%2F2G0ljf3');" class="tt"  href="http://twitter.com/intent/tweet?text=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C+http%3A%2F%2Fbit.ly%2F2G0ljf3" title="Post to Twitter"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/twitter/tt-twitter-micro4.png" alt="Post to Twitter" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C" title="Post to Digg"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/digg/tt-digg-micro4.png" alt="Post to Digg" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C" title="Post to Digg"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&t=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&t=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C" title="Post to Facebook"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/facebook/tt-facebook-micro4.png" alt="Post to Facebook" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&t=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&t=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C" title="Post to Facebook"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C&summary=%E3%81%AA%E3%81%9C%E3%81%8B%E3%80%81%2Fetc%2Frc.conf+%E3%81%AB%E4%BB%A5%E4%B8%8B%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%82%92%E3%81%97%E3%81%A6%E3%82%82%E5%8F%8D%E6%98%A0%E3%81%95%E3%82%8C%E3%81%AA%E3%81%84%E3%80%82%0A%0A%23ipv6_enable%3D%22YES%22%0Aipv6_network_interfaces%3D%22vtnet0%22%0Aipv6_ifconfig_vtnet0%3D%22inet6+2001%3A470%3Ad%3A461%3A%3A7%3A1+prefixlen+6...&source=電脳業務日誌');" class="tt"  href="http://www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C&summary=%E3%81%AA%E3%81%9C%E3%81%8B%E3%80%81%2Fetc%2Frc.conf+%E3%81%AB%E4%BB%A5%E4%B8%8B%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%82%92%E3%81%97%E3%81%A6%E3%82%82%E5%8F%8D%E6%98%A0%E3%81%95%E3%82%8C%E3%81%AA%E3%81%84%E3%80%82%0A%0A%23ipv6_enable%3D%22YES%22%0Aipv6_network_interfaces%3D%22vtnet0%22%0Aipv6_ifconfig_vtnet0%3D%22inet6+2001%3A470%3Ad%3A461%3A%3A7%3A1+prefixlen+6...&source=電脳業務日誌" title="Post to LinkedIn"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/linkedin/tt-linkedin-micro4.png" alt="Post to LinkedIn" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C" title="Post to Reddit"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/reddit/tt-reddit-micro4.png" alt="Post to Reddit" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2018/01/22/dragonfly-bsd-%e3%81%ae-ipv6-%e8%a8%ad%e5%ae%9a%e5%95%8f%e9%a1%8c/&title=DragonFly+BSD+%E3%81%AE+IPv6+%E8%A8%AD%E5%AE%9A%E5%95%8F%E9%A1%8C" title="Post to Reddit"> </a>
  </p>
</div>