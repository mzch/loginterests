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

```bash
ipv6_enable="YES"
ipv6_network_interfaces="vtnet0"
ipv6_ifconfig_vtnet0="inet6 2001:470:d:461::7:1 prefixlen 64"
ipv6_defaultrouter="2001:470:d:461::1"
```
仕方ないので、/etc/rc.local にコマンドを直書きしてごまかした。
```bash
#! /bin/sh
ifconfig vtnet0 inet6 2001:470:d:461::7:1 prefixlen 64 alias&lt;br />
route add -inet6 default 2001:470:d:461::1&lt;br />
```

~~解決法をご存じの方がいらしたら、ぜひコメントをお願いしたい。~~

追記。
  
メーリングリストで質問したら、ipv6\_ifconfig\_vtnet0 の設定がよくないと指摘された。
```diff
-ipv6_ifconfig_vtnet0="inet6 2001:470:d:461::7:1 prefixlen 64"
+ipv6_ifconfig_vtnet0="2001:470:d:461::7:1"
```
と、アドレスだけ指定するのが、DragonFly での作法とか。指摘してくれた、Aaron に感謝。
