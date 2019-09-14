---
title: Debian Stretch – GRUB 2 のバグ?
date: 2018-01-25T17:53:12+00:00
tweet_this_url:
  - http://bit.ly/2FfwIqa
categories:
  - Management
  - Server
  - Unix
tags:
  - Debian
  - Linux
draft: false
---
KVM のシリアルポート経由で、ブートメッセージをチェックするようにしているのだが、Debian Stretch をゲストにすると、なぜか GRUB 2 がシリアルコンソールにメニューを表示しない問題があった。

実用上さして気にするほどでもなかったので放置してたのだが、他のディストリビューション (CentOS 7, Ubuntu 16) ではちゃんと表示されるので、いっちょ修正するか、と手を出してみた。

~~結論。sid の GRUB 2 と入れ替えたら問題なく表示された。なぜ Stretch では直さないのかよくわからない。バックポートが難しいのだろうか。~~

<ins date="2018/03/03">使用している[スクリプト](https://github.com/mzch/vmmaestro)で kvm の起動待ちをしている部分が悪さをしていることがわかった。起動確認をしている間に grub メニューが表示されるため、シリアルコンソールに制御が移ったときには表示済みのため、一見表示されていないように見えただけだった。反省。</ins>
