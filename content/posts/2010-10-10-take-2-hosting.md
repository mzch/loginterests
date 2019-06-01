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

<div class="tweetthis" style="text-align:left;">
  <p>
    <a onclick="javascript:pageTracker._trackPageview('/outgoing/twitter.com/intent/tweet?text=Take+2+Hosting+http%3A%2F%2Fbit.ly%2FcKYirB');" class="tt"  href="http://twitter.com/intent/tweet?text=Take+2+Hosting+http%3A%2F%2Fbit.ly%2FcKYirB" title="Post to Twitter"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/twitter/tt-twitter-micro4.png" alt="Post to Twitter" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting" title="Post to Digg"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/digg/tt-digg-micro4.png" alt="Post to Digg" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting" title="Post to Digg"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2010/10/10/take-2-hosting/&t=Take+2+Hosting');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2010/10/10/take-2-hosting/&t=Take+2+Hosting" title="Post to Facebook"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/facebook/tt-facebook-micro4.png" alt="Post to Facebook" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2010/10/10/take-2-hosting/&t=Take+2+Hosting');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2010/10/10/take-2-hosting/&t=Take+2+Hosting" title="Post to Facebook"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting&summary=%E3%81%95%E3%81%A6%E3%80%81%E3%81%97%E3%81%8B%E3%81%97%E6%9D%B1%E6%B5%B7%E5%B2%B8%E3%81%AF%E3%81%A1%E3%82%87%E3%81%A3%E3%81%A8...%E3%81%9B%E3%82%81%E3%81%A6%E8%A5%BF%E6%B5%B7%E5%B2%B8%E3%81%AB%E3%81%82%E3%82%8C%E3%81%B0...%E3%81%A8%E3%81%84%E3%81%86%E6%96%B9%E3%82%82%E3%81%84%E3%82%89%E3%81%A3%E3%81%97%E3%82%83%E3%82%8B%E3%81%8B%E3%81%A8%E3%80%82%E3%81%9D%E3%82%93%E3%81%AA%E6%96%B9%E3%81%AB%E3%81%82%E3%81%A4%E3%82%89%E3%81%88%E3%81%9F%E3%82%88%E3%81%86%E3%81%AA%E3%83%97%E3%83%AD%E3%83%90%E3%82%A4%E3%83%80%E3%81%8C%E3%81%82%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82Take+2+Hosting+%E3%81%A7%E3%81%99%E3%80%82%0D%0A%0D%0A%0D%0A%E3%83%AD%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AF%E3%80%81%E3%82%B5%E3%83%B3%E3%83%8E%E3%82%BC+%28%E3%82%AB%E3%83%AA%E3%83%95%E3%82%A9%E3%83%AB%E3%83%8B%E3%82%A2%E5%B7%9E%29+%E3%81%A7%E3%81%93%E3%82%8C%E4%BB%A5%E4%B8%8A%E3%82%A2%E3%82%B8%E3%82%A2%E3%82%84%E3%82%AA%E3%83%BC%E3%82%B9%E3%83%88%E3%83%A9%E3%83%AA%E3%82%A2%E3%81%AB%E8%BF%91%E3%81%A5%E3%81%91%E3%82%8B%E3%81%AB%E3%81%AF%E3%80%81%E3%83%8F%E3%83%AF%E3%82%A4%E3%81%8B%E3%82%B0%E3%82%A2%E3%83%A0...&source=電脳業務日誌');" class="tt"  href="http://www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting&summary=%E3%81%95%E3%81%A6%E3%80%81%E3%81%97%E3%81%8B%E3%81%97%E6%9D%B1%E6%B5%B7%E5%B2%B8%E3%81%AF%E3%81%A1%E3%82%87%E3%81%A3%E3%81%A8...%E3%81%9B%E3%82%81%E3%81%A6%E8%A5%BF%E6%B5%B7%E5%B2%B8%E3%81%AB%E3%81%82%E3%82%8C%E3%81%B0...%E3%81%A8%E3%81%84%E3%81%86%E6%96%B9%E3%82%82%E3%81%84%E3%82%89%E3%81%A3%E3%81%97%E3%82%83%E3%82%8B%E3%81%8B%E3%81%A8%E3%80%82%E3%81%9D%E3%82%93%E3%81%AA%E6%96%B9%E3%81%AB%E3%81%82%E3%81%A4%E3%82%89%E3%81%88%E3%81%9F%E3%82%88%E3%81%86%E3%81%AA%E3%83%97%E3%83%AD%E3%83%90%E3%82%A4%E3%83%80%E3%81%8C%E3%81%82%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82Take+2+Hosting+%E3%81%A7%E3%81%99%E3%80%82%0D%0A%0D%0A%0D%0A%E3%83%AD%E3%82%B1%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3%E3%81%AF%E3%80%81%E3%82%B5%E3%83%B3%E3%83%8E%E3%82%BC+%28%E3%82%AB%E3%83%AA%E3%83%95%E3%82%A9%E3%83%AB%E3%83%8B%E3%82%A2%E5%B7%9E%29+%E3%81%A7%E3%81%93%E3%82%8C%E4%BB%A5%E4%B8%8A%E3%82%A2%E3%82%B8%E3%82%A2%E3%82%84%E3%82%AA%E3%83%BC%E3%82%B9%E3%83%88%E3%83%A9%E3%83%AA%E3%82%A2%E3%81%AB%E8%BF%91%E3%81%A5%E3%81%91%E3%82%8B%E3%81%AB%E3%81%AF%E3%80%81%E3%83%8F%E3%83%AF%E3%82%A4%E3%81%8B%E3%82%B0%E3%82%A2%E3%83%A0...&source=電脳業務日誌" title="Post to LinkedIn"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/linkedin/tt-linkedin-micro4.png" alt="Post to LinkedIn" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting" title="Post to Reddit"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/reddit/tt-reddit-micro4.png" alt="Post to Reddit" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2010/10/10/take-2-hosting/&title=Take+2+Hosting" title="Post to Reddit"> </a>
  </p>
</div>