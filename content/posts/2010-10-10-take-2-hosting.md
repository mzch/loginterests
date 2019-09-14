---
title: Take 2 Hosting
author: mzch
type: post
date: 2010-10-09T16:01:44+00:00
url: /2010/10/10/take-2-hosting/
tweet_this_url:
  - http://bit.ly/cKYirB
categories:
  - Dedicated Server
  - Server
tags:
  - Dedicated Server
  - 専用サーバー

---
さて、しかし東海岸はちょっと&#8230;せめて西海岸にあれば&#8230;という方もいらっしゃるかと。そんな方にあつらえたようなプロバイダがあります。<a onclick="javascript:pageTracker._trackPageview('/outgoing/www.take2hosting.com/');"  href="https://www.take2hosting.com/">Take 2 Hosting</a> です。

ロケーションは、サンノゼ (カリフォルニア州) でこれ以上アジアやオーストラリアに近づけるには、ハワイかグアムにでもデータセンターを置くしかない。そんなことするなら、シンガポールに置きますやね。まあ、それはともかく、ここの特徴はデリバリーが早い! ことと、完全に自動化された保守ツールにあります。 

まず、サーバーの電源ON/OFF、再起動は独自のコントロールパネルから簡単に行うことができます。ここがすごいと思うのは、OS の再インストールまでコントロールパネルでできてしまうところです。再インストールしたい OS と RAID の有無や種類を選択してボタンをクリックするだけという、まるで VPS みたいな操作性です (実際には誤操作防止のために決められたキーワードを入力しなくてはならないのですが)。 

<div id="attachment_1164" style="width: 310px" class="wp-caption alignnone">
  <a onclick="javascript:pageTracker._trackPageview('/outgoing/daybook.biz/wp-content/uploads/2010/10/Take-2-Hosting-Server-Controls.png');"  href="http://daybook.biz/wp-content/uploads/2010/10/Take-2-Hosting-Server-Controls.png"><img aria-describedby="caption-attachment-1164" src="http://daybook.biz/wp-content/uploads/2010/10/Take-2-Hosting-Server-Controls-300x288.png" alt="Take 2 Hosting Server Controls" title="Take 2 Hosting Server Controls" width="300" height="288" class="size-medium wp-image-1164" srcset="https://daybook.biz/wp-content/uploads/2010/10/Take-2-Hosting-Server-Controls-300x288.png 300w, https://daybook.biz/wp-content/uploads/2010/10/Take-2-Hosting-Server-Controls-1024x985.png 1024w, https://daybook.biz/wp-content/uploads/2010/10/Take-2-Hosting-Server-Controls.png 1239w" sizes="(max-width: 300px) 100vw, 300px" /></a>
  
  <p id="caption-attachment-1164" class="wp-caption-text">
    こんな感じです
  </p>
</div>

さらに、リモートKVMはありませんが、サーバーごとにターミナルサーバーのアカウントが割り振られており、SSH 経由でシリアルポートにアクセスすることができます。OS のコンソールはもちろん、BIOS の出力もディフォルトでシリアルポートに割り当てられていますので、上記のコントロールパネルとあわせて KVM と同じ＝ローカルコンソールと同じことができるようになっています。実際、これだけあればほとんどサポートに頼ることなくサーバーの運用が可能です。 

また、ディスクが <span style="color:red;">RAID 前提</span>で最低でも 2 組装着されているのもポイント高いです。 

回線は標準が、下り（サーバーからのダウンロード）10Mbps unmetered で、上り（サーバーへのアップロード）は制限がありません。ストリーミングする人には心もとない帯域ですが、その場合は追加費用を払って回線をアップグレードして頂くしか。^^; 50Mbps と 100Mbps がメニューにあります。 

ここもサポートがしっかりしており、海外のサーバーを初めて借りるという方でも安心してお勧めできます。が、一度運用を始めたら、ものすごく安定してるので、ピンポイントにハードウェア障害とか起きたりしない限り、サポートのお世話になることなんてほとんどないんじゃないでしょうか。私は一度ディスクを大容量のものに換装してもらうためにチケットを切ったことがあるだけで、ほかにサポートへ連絡する必要が生じたことはありませんでした。 

惜しむらくは、優良なプロバイダであるがゆえに、<span style="color:red; font-weight:bold; font-size:large;">売り切れが多い</span>という点です。現に今も完売状態です。アメリカ西海岸のサーバーを検討していて、ここに在庫があれば、迷わず申し込んだほうがいいです。
