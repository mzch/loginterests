---
title: JIRA と Confluence
date: 2009-04-22T18:29:53+00:00
draft: false
categories:
  - Management
  - Web
tags:
  - Confluence
  - JIRA
  - Wiki
  - バグトラッカー
  - プログラム開発
  - マネージメント
---
[Atlassian](http://www.atlassian.com/starter/?s_kwcid=HM_Starter) が、一年間のサポートつきで、同社の製品、[JIRA](http://www.atlassian.com/software/jira/) と [Confluence](http://www.atlassian.com/software/confluence/) を期間限定で、$5 USDで販売している。

JIRA は、エンタプライズユースのバグトラッカーシステム。
  
Confluence は、エンタープライズグレードの Wiki システム。

通常のコマーシャル価格を見ると、一番安い Teamエディションでも、$1,200 USDはするしろものです。それを[チャリティ](http://www.roomtoread.org/)用のスターターエディション (5ユーザまで)とはいえ、$5ドルというのは太っ腹! こんなこと、日本のメーカーにはできんですなぁ。足下固まってるからできることなんでしょうね。うらやましい。

で、一応買いました。両方とも。だってそれでも $10 USD なんだもん。お客さんのバグ報告がダイレクトにわかる、[Get Satisfiction!](http://www.getsatisfaction.com/) なんかの方がダイナミックでよいところも多いのですが、大抵は、問題があるぞー! ちょっと待って&#8230;うん、直った。ありがとー! じゃねー。的な応酬なんで、バグ記録という意味ではきちんとした資料にできるかというのがちょーっと不安で。でもオープンソースのはなぜか軒並み使いにくい&#8230;いやー。速攻で買いました。零細なので充分です。^^;

どちらも Java で書かれてて、普通にインストールする分には何も悩むところはありません。ま、実際は、Apache + mod_mk でリクエストをリダイレクトして&#8230;とかして使うんでしょうけど、それもまあさほど悩むようなものでもない。本当、インストールガイド通り。

ただし、なぜか SSL ではまってしまいました。OpenSSL で作った秘密鍵をどうしてもキーストアに読み込もうとしない。もうね、あちこち調べて何時間もかけて、わからずじまい。サポートに聞くという手ももちろんあるんですが、どうせ Apache 通さないといけなかったので、諦めました。

で、mod_jk を導入して、ちょろっとリダイレクト設定すると、全く問題なくサイトが立ち上がりました。やー。既製品はこういうとこ楽やわー。後は、セットアップウィザードの指示に従って必要事項を埋めればインストール完了で、使えるようになりました。途中、意地になって、Tomcat のキーストアに OpenSSLの秘密鍵を読み込む方法を探し回ったりしなければ、確認と試運転入れても二時間ってとこでしょうか。まだこれから使い込んでいくんですが、表面をなでた感じでは、悪くないです。というか、しっかり作り込まれています。まあ、細かいことを言い出すときりがないんですが、認証のとこだけ SSL を通すことができるようになっててもよかったんじゃないかなぁと思うんですけどねぇ。ま、それは自前でシングルサインオンのプラグインを書けってことなんでしょうね。あるいはサードパーティのプラグインを買うか。でも $5 でいいのかなこれ。ってくらいきちんとしたソフトですよ。間違いなくお買い得。

ソフト開発のマネージメントが必要な人以外意味のないソフトですが、いる人にはいるものなので、見るだけ見てみてはいかがでしょう。なお、このキャンペーンは、五日間だけで、4/25 (多分、アメリカ東海岸時間だと思う) には終了しますので、お試しはお早めに。:)

<div class="tweetthis" style="text-align:left;">
  <p>
    <a onclick="javascript:pageTracker._trackPageview('/outgoing/twitter.com/intent/tweet?text=JIRA+%E3%81%A8+Confluence+http%3A%2F%2Fbit.ly%2FdEuvZZ');" class="tt"  href="http://twitter.com/intent/tweet?text=JIRA+%E3%81%A8+Confluence+http%3A%2F%2Fbit.ly%2FdEuvZZ" title="Post to Twitter"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/twitter/tt-twitter-micro4.png" alt="Post to Twitter" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence" title="Post to Digg"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/digg/tt-digg-micro4.png" alt="Post to Digg" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/digg.com/submit?url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence');" class="tt"  href="http://digg.com/submit?url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence" title="Post to Digg"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&t=JIRA+%E3%81%A8+Confluence');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&t=JIRA+%E3%81%A8+Confluence" title="Post to Facebook"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/facebook/tt-facebook-micro4.png" alt="Post to Facebook" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.facebook.com/share.php?u=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&t=JIRA+%E3%81%A8+Confluence');" class="tt"  href="http://www.facebook.com/share.php?u=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&t=JIRA+%E3%81%A8+Confluence" title="Post to Facebook"> </a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence&summary=Atlassian+%E3%81%8C%E3%80%81%E4%B8%80%E5%B9%B4%E9%96%93%E3%81%AE%E3%82%B5%E3%83%9D%E3%83%BC%E3%83%88%E3%81%A4%E3%81%8D%E3%81%A7%E3%80%81%E5%90%8C%E7%A4%BE%E3%81%AE%E8%A3%BD%E5%93%81%E3%80%81JIRA+%E3%81%A8+Confluence+%E3%82%92%E6%9C%9F%E9%96%93%E9%99%90%E5%AE%9A%E3%81%A7%E3%80%81%245+USD%E3%81%A7%E8%B2%A9%E5%A3%B2%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E3%80%82%0D%0A%0D%0A%C2%A0%0D%0AJIRA+%E3%81%AF%E3%80%81%E3%82%A8%E3%83%B3%E3%82%BF%E3%83%97%E3%83%A9%E3%82%A4%E3%82%BA%E3%83%A6%E3%83%BC%E3%82%B9%E3%81%AE%E3%83%90%E3%82%B0%E3%83%88%E3%83%A9%E3%83%83%E3%82%AB%E3%83%BC%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%80%82%0D%0AConfluence+%E3%81%AF%E3%80%81%E3%82%A8%E3%83%B3%E3%82%BF%E3%83%BC%E3%83%97%E3%83%A9%E3%82%A4%E3%82%BA%E3%82%B0%E3%83%AC%E3%83%BC%E3%83%89%E3%81%AE+Wiki+%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%80%82%0D%0A...&source=電脳業務日誌');" class="tt"  href="http://www.linkedin.com/shareArticle?mini=true&url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence&summary=Atlassian+%E3%81%8C%E3%80%81%E4%B8%80%E5%B9%B4%E9%96%93%E3%81%AE%E3%82%B5%E3%83%9D%E3%83%BC%E3%83%88%E3%81%A4%E3%81%8D%E3%81%A7%E3%80%81%E5%90%8C%E7%A4%BE%E3%81%AE%E8%A3%BD%E5%93%81%E3%80%81JIRA+%E3%81%A8+Confluence+%E3%82%92%E6%9C%9F%E9%96%93%E9%99%90%E5%AE%9A%E3%81%A7%E3%80%81%245+USD%E3%81%A7%E8%B2%A9%E5%A3%B2%E3%81%97%E3%81%A6%E3%81%84%E3%82%8B%E3%80%82%0D%0A%0D%0A%C2%A0%0D%0AJIRA+%E3%81%AF%E3%80%81%E3%82%A8%E3%83%B3%E3%82%BF%E3%83%97%E3%83%A9%E3%82%A4%E3%82%BA%E3%83%A6%E3%83%BC%E3%82%B9%E3%81%AE%E3%83%90%E3%82%B0%E3%83%88%E3%83%A9%E3%83%83%E3%82%AB%E3%83%BC%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%80%82%0D%0AConfluence+%E3%81%AF%E3%80%81%E3%82%A8%E3%83%B3%E3%82%BF%E3%83%BC%E3%83%97%E3%83%A9%E3%82%A4%E3%82%BA%E3%82%B0%E3%83%AC%E3%83%BC%E3%83%89%E3%81%AE+Wiki+%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%80%82%0D%0A...&source=電脳業務日誌" title="Post to LinkedIn"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/linkedin/tt-linkedin-micro4.png" alt="Post to LinkedIn" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence" title="Post to Reddit"><img class="nothumb" src="https://daybook.biz/wp-content/plugins/tweet-this/icons/en/reddit/tt-reddit-micro4.png" alt="Post to Reddit" /></a> <a onclick="javascript:pageTracker._trackPageview('/outgoing/reddit.com/submit?url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence');" class="tt"  href="http://reddit.com/submit?url=https://daybook.biz/2009/04/23/jira-%e3%81%a8-confluence/&title=JIRA+%E3%81%A8+Confluence" title="Post to Reddit"> </a>
  </p>
</div>