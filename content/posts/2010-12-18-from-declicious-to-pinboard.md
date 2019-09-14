---
title: Declicious から Pinboard へ
author: mzch
type: post
date: 2010-12-17T17:41:18+00:00
url: /2010/12/18/from-declicious-to-pinboard/
tweet_this_url:
  - http://bit.ly/gupUyN
categories:
  - Cloud service
  - Mac
  - Web
tags:
  - Bookmarks
  - Delibar
  - Delicious
  - Pinboard
  - Pukka
  - Quiet Read
  - ブックマーク

---
既にご存じの方も多いと思われますが、[TechCrunch Japan](http://jp.techcrunch.com/archives/20101216is-yahoo-shutting-down-del-icio-us/)でも報道されている通り、[Yahoo!(http://www.yahoo.com/) は、[Delicious](http://www.delicious.com/) を~~廃止すると決定しました~~売却する予定だと発表しました。（12/22 更新)

まあ [Yahoo!](http://www.yahoo.com/) ですし、買収した事業でまともに継続できてるものがあるのか? といった会社ですから、仕方ないのですが、ユーザーは大混乱。そりゃまあそうですよね。で、そんな人に朗報。Yahoo! の元社員が作ったシンプルながら必要な機能は揃っているという、[Pinboard](http://pinboard.in/) があります。

昨年始まったサービスなのですが、当初は副業だったはずが、順調にユーザー数を伸ばし、今やフルタイムで取りかかっているとか。ただし<span style="font-size:large; font-weight:bold; color:red;">無料じゃありません</span>。登録費用が、<span style="color:blue;">今現在で $7.85</span> かかります。これ、後になればなるほど<span style="color:red;">値段が上がっていく</span>という (サービス開始時のβ版の時は、$2.84) ユニークな値付けポリシーなので、早めに登録した方がよろしいかと。:)


と言ってもクライアントが対応してなきゃなぁと思うあなた。Windows は知らないので何とも言えませんが、Mac ならちゃんと対応したソフトがあります。

まずは、[Delibar](http://www.delibarapp.com/)。[Delibar](http://www.delibarapp.com/) は、単にアカウントを追加するだけです。超オススメ。どんなものか詳しく! という方は私のショボい説明より、[Macの手書き説明書さんの記事](http://veadardiary.blog29.fc2.com/blog-entry-717.html")や、[わかばマークのMacの備忘録さんの記事](http://wakabamac.blog95.fc2.com/blog-entry-602.html)をご覧下さい。もしくは、[linkerさんのレビュー](http://linker.in/journal/2009/12/deliciousdelibar.php)とか。[soundscape out さんの記事](http://d.hatena.ne.jp/tanemori/20091022/Delibar)もあります。

[Delicious](http://www.delicious.com/) クライアントではありませんが、[Quiet Read](http://bambooapps.com/free-stuff/) も [Pinboard](http://pinboard.in/) に対応しています。ブックマークしたURLをメニューから簡単に [Pinboard](http://pinboard.in/) へ (もちろん、[Delicious](http://delicious.com/) や、[Instapaper](http://www.instapaper.com/)、[Read It Lator](http://readitlaterlist.com/) にも) 送信できます。わざわざブクマするほどではないけど、後で読むので URL を保存しておきたいという向けのツールです。レビューは、[Macの手書き説明書さんの記事](http://veadardiary.blog29.fc2.com/blog-entry-2543.html)や、[MacOSXの新着アプリテスト記録とトラブルシューティングさんの 7月17日付けのレビュー](http://nmuta.fri.macserver.jp/unei1007a.html)をどうぞ。

あとひとつ、[Pukka](http://codesorcery.net/pukka) も対応可能です。ただし、[Delicious](http://www.delicious.com/) アカウントと [Pinboard](http://pinboard.in/) アカウントは<span style="font-size:large; font-weight:bold; color:red;">同居できません</span>。対応方法は次の通り。

  1. Preferences を開いて、Accounts で、既存のアカウントを削除します。
     ![Pukka: Preferences - Accounts](wp-content/uploads/2010/12/Pukka001.png)

 
  1. 次に、Preferences の Advanced を開きます。 
  1. API URL: の欄に、[https://api.pinboard.in/v1](https://api.pinboard.in/v1) と入力します。
     ![Pukka: Preferences - Advanced](/wp-content/uploads/2010/12/Pukka002.png)

  1. 再び Accounts を開いて、[Pinboard](http://pinboard.in/) のユーザーアカウント情報を入力します。 

もちろんブックマークレットもありますので、クライアントは使わないって人だって安心です。どうです? 興味が湧きました? でも実は [Pinboard](http://pinboard.in/) の魅力はこれだけではないのです。<span style="font-size:large; font-weight:bold; color:blue;">年$25 のサブスクリプション</span>になりますが、なんと<span style="font-size:large; font-weight:bold; color:red;">ブックマークしたページを自動的に取得してサーバー上に保存する</span>ことができるのです。そう、[ウェブ魚拓](http://megalodon.jp/)みたいなものにもなるんですよ。頻繁に使うんだけど最近[ウェブ魚拓](http://megalodon.jp/)が遅いとか重いとか不満なあなたに是非!

で、肝心の Delicious から Pinboard へのブックマークの移行ですが、次のようにします。

  1. まず、[Delicious](http://www.delicious.com/) にログインして、[Settings](https://secure.delicious.com/settings/) 画面を開き、Bookmarks 欄の2番目にある [Export / Backup Bookmarks](https://secure.delicious.com/settings/bookmarks/export) リンクをクリックします。 
  1. [Export / Download Your Delicious Bookmarks](https://secure.delicious.com/settings/bookmarks/export) 画面が開きますので、下の方にある Export ボタンをクリックします。 
  1. 保存場所を尋ねられたらどこにブックマークファイルを保存するか指定して、(このへんはブラウザの設定次第です) ブックマークファイルがダウンロードします。 
  1. 次に、[Pinboard](http://pinboard.in/) にログインして、[Settings](http://pinboard.in/settings/) 画面を開きます。 
  1. [Import](http://pinboard.in/settings/import) タブをクリックして、[Import](http://pinboard.in/settings/import) 画面を開きます。 
  1. Select the file that contains your bookmarks: の横にある「ファイルを選択」ボタンをクリックして、[Delicious](http://www.delicious.com/) からダウンロードしたブックマークファイルを指定します。 
   1. Click &#8216;Upload&#8217; and wait for the bookmarks to upload. の下にある「Upload」ボタンをクリックします。 
   1. すると、一番下の Your previous imports: という行のさらに下に、インポートの状況が示されます。Uploaded が、アップロードした日時、status が処理状況 (最初は、Pending になります) 
   1. 後は、慌てず騒がずインポート処理が完了するのは待つだけです。

いかがでしょう。移行がちょっと手間ですけど、よいサービスですよ。まだまだ精力的に開発が続いているので、ホントお勧めです。何より有料なので<span style="font-size:large; font-weight:bold; color:blue;">スパマーが来ない</span>というのが。:)


>2010年12月17日-18日時点で、ネットワーク負荷がかなり高くなっており、ブックマークのインポートなどが遅延しているとメッセージが表示されています。Delicious 廃止を受けてユーザーが殺到しているのかも知れません。
