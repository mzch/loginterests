---
title: "Mongodb のレプリカセットで嵌まったこと"
date: 2019-06-20T17:27:01+09:00
categories:
  - Server
  - Database
tags:
  - MongoDB
  - NoSQL
  - Server
  - サーバー
draft: true
---

MongoDB 4.0.10 で、レプリカセットを作成しようとして、PRIMARY ノードで、

```mongo
rs.initiate()
rs.add("192.168.0.2")
rs.add({host:"192.168.0.3",arbiterOnly:true})
```

とかやって、SECONDARY と ARBITER を追加したら、なぜか両者ともステータスが、「STARTUP」から変わらない。おかしいな、と思って、三つともインスタンスを再起動したら、今度は PRIMARY のはずのノードが「OTHER」になってしまった。

ググってみるも似たような症例はなく、悩んだのだが、次のようにしたら、解決した。

```mongo
var config = {
  _id : "rs01",
  members: [
    { _id: 0, host: "192.168.207.12:27017" },
    { _id: 1, host: "192.168.207.112:27017" },
    { _id: 2, host: "192.168.207.113:27017", arbiterOnly: true },
  ]
}
rs.initiate(config)
```

rs.add との違いはわからず。[公式ドキュメントにも記載されている方法](https://docs.mongodb.com/manual/reference/method/rs.add/)なのに、なぜこれがダメで、下の方法だとうまくいったのか… Docker 経由で使ってるからか、自分自身もちゃんと add しなくちゃならないのか、何とも言えず、もやっとしている。
