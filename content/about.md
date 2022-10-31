---
title: "私ですか?"
date: "2019-05-31"
draft: false
---

詳しくは、[こちら](https://mcuce.com/@mzch)をどうぞ。

何か言伝があるのでしたら、以下のフォームをお使いください。

<br />
<script src="https://www.google.com/recaptcha/api.js" async defer></script>
<form action="https://submit-form.com/6XTvdIOM" method="POST"  target="_blank">
  <p>
  <label for="name">お名前</label>
  <input type="text" id="name" name="name" placeholder="" required="" style="background-color:#f0f0f0; width:100%" /></p>
  <p>
  <label for="email">メール</label>
  <input type="email" id="email" name="email" placeholder="example@example.jp" required="" style="background-color:#f0f0f0; width:100%;" /></p>
  <p>
  <label for="message">メッセージ</label><br />
  <textarea
    id="message"
    name="message"
    placeholder="何でもお書き下さい。"
    required="true"
    style="background-color:#f0f0f0; width:100%; height:8em;"
  ></textarea></p>
  <p><div
    class="g-recaptcha"
    data-sitekey="6Lcqne0UAAAAAIDQsmv0mX7PlXGJpImoBuIYPm64"
    data-callback="callback"
  ></div></p>
  <button type="submit" id="submit-button" style="padding:5px 20px 5px 20px; color:white; background-color:gray;">送信</button>
</form>

<script type="text/javascript">
      function callback() {
        const submitButton = document.getElementById("submit-button");
        submitButton.removeAttribute("disabled");
      }
</script>
