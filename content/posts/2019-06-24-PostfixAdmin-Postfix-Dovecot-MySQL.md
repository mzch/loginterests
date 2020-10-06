---
title: "Postfix, Dovecot and MySQL"
date: 2019-06-24T12:50:31+09:00
categories:
  - Server
  - サーバー
  - Mail
  - メール
tags:
  - Postfix
  - PostfixAdmin
  - Dovecot
  - MySQL
draft: false
---
[Postfix](http://www.postfix.org/) と [Dovecot](https://www.dovecot.org/) を使って、メールサーバーを運用しているのだが、うちは構成が少し変則的で、メール送信サーバー (__SMTP__) とメール受信サーバー (__IMAP/POP3__) が分離している。最終的なメールの配送は [Dovecot](https://www.dovecot.org/) の [LMTP](https://wiki.dovecot.org/LMTP) デーモンに頼っているのだが、エイリアスにメールが配送されないという問題が発覚した。


~~別にバグでも何でもなく、ただの構成ミスである。[Dovecot](https://www.dovecot.org/) の仮想メールボックス機能を使ってメールアドレスを管理しているのだが、当初、[Postfix](http://www.postfix.org/) の送信サーバーと [Dovecot](https://www.dovecot.org/) の受信サーバーは同居していたので、ローカルの配送は、[Postfix](http://www.postfix.org/) の Virtual [Transport](http://www.postfix.org/transport.5.html) に任せていた。この時点では、エイリアスの処理も問題なかった。~~

~~最近、サーバーの移転を行ったのにあわせて、送信サーバーと受信サーバーの分離を行ったのだが、これは、ローカル配送に Dovecot の [LMTP](https://wiki.dovecot.org/LMTP) デーモンが使えることがわかったからである。で、何も考えずに移行して嵌まった、と。~~

~~アドレス管理のバックエンドに MySQL を使い、[PostfixAdmin](http://postfixadmin.sourceforge.net/) で Web から管理していたのだが、それ自体はまあついで。問題は、[LMTP](https://wiki.dovecot.org/LMTP) に配送を移したことで、[Postfix](http://www.postfix.org/) の Virtual [Transport](http://www.postfix.org/transport.5.html) が解釈されなくなってしまったことにある。別ソフトなんだから、当たり前ですな。そのため、MySQL で管理していたエイリアス情報が参照されなくなってしまい、__未達__になっていた、と。~~

~~多分、色んな解決法があるんでしょうけど、バックエンドに MySQL を使っている私の場合は、[Dovecot](https://www.dovecot.org/) のユーザー情報取得部分に手を入れることで、部分的に解決した。具体的には、ユーザー情報を MySQL から取得するクエリー文を以下のように修正しただけ。~~

```sql
user_query =
  SELECT concat('/var/mail/', maildir) as mail,
         concat('*:bytes=', quota) as quota_rule,
         998 as uid,
         8 as gid
  FROM mailbox WHERE
    active = '1' AND
    username =
        (SELECT goto FROM alias WHERE
            (address = '%u' AND alias.active = '1') OR
            (address = (SELECT concat('%n', '@', target_domain) FROM alias_domain
                        where alias_domain = '%d' AND alias_domain.active = '1'
                       )
            )
        )
```

~~[PostfixAdmin](http://postfixadmin.sourceforge.net/) は、メールボックスの情報もエイリアステーブルに書き込んでくれるので (その場合、エイリアスとメールボックスに同じ値が入る)、通常のメールボックス宛てのメールもこれでちゃんと読み書きできる。ということで。メールアドレスのエイリアスとドメインのエイリアスはこれで解決したが、外部のアドレスに対する転送だけはどうしようもなかった。[LMTP](https://wiki.dovecot.org/LMTP) にその機能がないので。~~

[2019/07/20 追記]
LMTP 全然関係なかった。なぜか、`receive_override_options = no_address_mappings` という行が、`main.cf` に紛れ込んでいて、こいつのせいで、Alias 展開が阻害されていたという…いつこんな記述を加えたのか…恥ずかしいっ。