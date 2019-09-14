---
title: Dedicated Lime
author: mzch
type: post
date: 2010-10-07T18:44:31+00:00
url: /2010/10/08/dedicated-lime/
tweet_this_url:
  - http://bit.ly/arqb3t
categories:
  - Dedicated Server
  - Server
tags:
  - Dedicated Server
  - 専用サーバー

---
何年か前から海外の専用サーバーを借りる機会があって、主にアメリカのサーバーをよくチェックしてるんですが、お値段が比較的安価で、回線容量もそこそこ、安定性も合格点と三拍子そろったプロバイダはなかなかありません。しかし、やはり探せばあるもので、今現在個人的にイチオシなのが、<a onclick="javascript:pageTracker._trackPageview('/outgoing/dedicatedlime.com/');"  href="http://dedicatedlime.com/">Dedicated Lime</a> というプロバイダです。もちろん、私自身使用しています。

ロケーションがアトランタ (ジョージア州) とほとんど東海岸なので、日本から ping を打つと、応答が大体 180ms-190ms と、ちょっと遠いのが難点といえば難点ですが、当然、それを補って余りある利点があります。 

まず、安い。ハードウェアに HP ® Proliant を使用しており、Xeon 3.0Ghz (P4世代) x 2、メモリ3GB、起動用の内蔵ディスクとは別に <span style="color:blue;">RAID-1 構成の SANディスクが 300GB</span>、<span style="color:red;">リモート KVM が付属</span>して (<span style="color:red; font-weight:bold">←これ重要</span>)、月々 <span style="font-size:large; font-weight:bold;">$89</span> です。もちろん、もっと最近のモデルもラインアップには揃えられています。 

ハードディスクというのはやはりサーバーを構成するパーツの中ではどうしても壊れやすく、いくらバックアップをとってあったとしてもクラッシュしてしまえばある程度のダウンタイムが発生してしまいます。バックアップからクラッシュまでの間に更新があったとしたら取り戻しようがないのも悩みのたね。まさかそのためにフォールトトレラントを構成するわけにもいきません。そこで比較的安価でプロバイダーも対応が慣れている RAID を構成することでその危険を少しでも小さくするというのが、私がサーバーを構成する時の基本になっています。ごく小規模のサーバーにおいて、ハードウェア RAID か、ソフトウェア RAID かというのは今どき問題になりませんが、そもそもディスクをふたつ装着するのに高い別料金をとるところが多いこと多いこと。 

その点、ここ <a onclick="javascript:pageTracker._trackPageview('/outgoing/dedicatedlime.com/');"  href="http://dedicatedlime.com/">Dedicated Lime</a> は RAID-1 前提の構成なので<span style="color:red; font-weight:bold; font-size:large;">安心</span>できるわけですね。 

ハードウェアでいえばもう一点。<span style="color:red">リモートＫVMが付属</span>していることが大きいです。リモートメディアマウント機能つきですから、辛抱強い人であれば自力で OS のインストールを行うことができます。まあ実際はファイアウォールの設定をミスって SSH でログインできなくなったとか、BIOSの設定を変更したいとか、ローカルコンソールがないとどうしようもない状況に陥った時に出番なんですが、そんなときでも安心なわけです。これ、普通のプロバイダだと安いところでもつけたら最低でも月々 $40 以上はかかります。

次に回線。<a onclick="javascript:pageTracker._trackPageview('/outgoing/www.WebHostingTalk.com');"  href="http://www.WebHostingTalk.com">WebHostingTalk.com</a> のオファーセクションをずらっと眺めてみてください。同価格帯のサーバーですと、月転送量が 2000GB とか、3000GB というところが多いのですが、<a onclick="javascript:pageTracker._trackPageview('/outgoing/dedicatedlime.com/');"  href="http://dedicatedlime.com/">Dedicated Lime</a>は、<span style="color:red; font-weight:bold; font-size:large;">100Mbps Unmetered</span> です! 共有回線なので、最低保証は上り下り合わせて6000GB となりますが、いちいち転送量を気にしなくてもよいというのは精神衛生上、非常に重要なことです。

そして、何よりもここをオススメする一番の理由は、<span style="color:blue; font-weight:bold; font-size:large">サポートが丁寧</span>なことです。私の下手糞な英語に対してきちんきちんと応対してくれます。借りる前も借りた後もそれは変わりません。中の人一人で担当しているらしくすぐに返事が返ってこないこともありますが、長時間の放置はありません。対応もこちらの意図を汲んで的確に行ってくれます。 

最後に安定性。今年の1月から3月にかけて、月一ペースでデータセンターで障害があったのですが、状況を逐一報告してくれてユーザーとしては安心していることができました。今はそんなこともなく、安定運用に戻っています。全く問題は起きていません。 

いかがでしょう。日本の低スペックで高いサーバーで我慢されているなら、こちらのサーバを検討した方がいいと思いますよ。
