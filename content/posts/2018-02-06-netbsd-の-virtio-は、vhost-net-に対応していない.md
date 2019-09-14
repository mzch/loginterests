---
title: NetBSD の virtio は、vhost-net に対応していない
date: 2018-02-06T09:10:45+00:00
tweet_this_url:
  - http://bit.ly/2BGBxLo
categories:
  - Server
  - Unix
  - VPS
tags:
  - BSD
  - NetBSD
  - Unix
draft: false
---
調子に乗って、[NetBSD](http://netbsd.org/) もインストールしてみた。

最初、ネットワークアダプタを認識してるのに外部へも外部からも通信できなくて頭を捻ったのだが、kvm の vhost-net を off にしたら問題なく通信するようになった。他の BSD が vhost-net に対応していたので、これはちょっと意外。
