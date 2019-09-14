---
title: Pydio Cells の隠し仕様
date: 2019-01-15T09:11:02+00:00
tweet_this_url:
  - http://bit.ly/2Cl4bjb
categories:
  - Server
  - Software
  - Sync / Backup
  - Unix
  - VPS
  - Web
tags:
  - File sharing
  - Linux
  - Unix
draft: false
---
ファイル共有サーバーソフト、[Pydio](https://pydio.com/) が、内容を一新、Go でスクラッチから書き直されて、[Pydio Cells](https://pydio.com/en/features) となった。

最近になって、更新のための時間が取れたので、インストールしてみた。ところ、このブログも乗っかってる専鯖上の VM には問題なくインストール完了。ところが、ストレージ目的で借りている VPS で、所謂ヌルポインタエラーが出た。フォーラムで質問しても解決しなかったが、うまくいったケースとそうでないケースを見比べて違いを埋めていった結果、[Pydio Cells](https://pydio.com/en/features) は、プライベート IP アドレスがないとセグメンテーションフォールトを起こす仕様になっていることがわかった。

[ドキュメント](https://pydio.com/en/docs/cells/v1/installation-guides)のどこにも書いてないが、[ソースではしっかりチェックされてて、確かにプライベートアドレスがないとエラーになる箇所](https://github.com/pydio/cells/blob/master/vendor/github.com/micro/go-web/service.go)があった。ところがそのエラーをチェックせずに実行を継続しているので所謂ぬるぽになっている。明らかなバグ。[フォーラム](https://forum.pydio.com/t/pydio-cells-not-working/1182/38)で報告しておいた。

<ins datetime="2019-03-15T19:00:00+9:00">[2019/03/15 追記] バージョン 1.4 でこの問題が解決されていることを確認しました。</ins>
