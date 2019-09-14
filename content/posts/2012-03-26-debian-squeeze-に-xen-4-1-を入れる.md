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
