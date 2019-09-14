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
```bash
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
```bash
    sudo firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv4" source address="118.243.217.235" accept'
```
```bash
    sudo firewall-cmd --permanent --zone=public --add-rich-rule='rule family="ipv6" source address="2405:6584:7840:800::/64" accept'
```
内部通信用のインターフェースは無条件で信頼する。
```bash
    sudo firewall-cmd --permanent --zone=trusted --add-interface=eth1
```
設定をリロードして、おしまい。
```bash
    sudo firewall-cmd --reload
```
と思ったら、内部インターフェースが起動されていなかったので、NetworkManager で起動させる。
```bash
    sudo nmcli c m eth1 connection.autoconnect yes
    sudo nmcli c modify eth1 ipv4.addresses 192.168.207.110/24
```
