---
layout: post
---

役生一次 175 日 用 Final Cut Pro 後製不出 H.264 縮時影片？
---

<br>

原本我是用 Adobe Premiere 在把 Gopro 拍的縮時照片做成影片的，但在買了 Final Cut Pro 後，當然就要改用 FCP 啦

恩，不過在今天之前卻一直是有個大問題的 ＝～＝

<br>

Gopro 照出來的照片我通常選的是 12MP = 4000 x 3000 pixel，因此把照片一股腦地拖進 FCP 後

很直覺地會在 Project 的設定中弄一個 Cusmtom 出來

<img src="{{site.url}}/img/2015-05-13/setting.jpg" width="50%">

接著就把每張照片的 Duration 調成 1s，然後 Share（在 FCP 裡的 Export 叫做 Share）

之前在 PE 我都是 Export 成 H.264 的 .mp4，但在 FCP 裡面我都得先 Export 成 .mov 再用 ffmpeg 去轉成 .mp4

<img src="{{site.url}}/img/2015-05-13/h264.png" width="45%">

恩，到這邊好像都一切順利，然後按下 Next

<img src="{{site.url}}/img/2015-05-13/fail.jpg" width="35%">

... ＝＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＝

去查 error code 根本查不到什麼東西，也找不到一樣遇到這種問題的人，嘗試了一陣子覺得無解後，只好改用 Source - Apple ProRes 422 來 Export

<img src="{{site.url}}/img/2015-05-13/prores422.png" width="45%">

但這樣檔案就變得崩潰大呀 Ｑ＿＿＿＿＿＿＿＿＿Ｑ

<br>

## 終於，直到今天，正當我心血來潮地(其實是終於想到了)把蘭嶼的影片拿出來整理時

意外發現，原來只要改改 Project 的 Setting

<img src="{{site.url}}/img/2015-05-13/success.jpg" width="40%">

就可以成功 Export 囉（暈）

## 原來 H.264 還需要特定的 Resolution 才能 Encode 呀...

<br>

## 後記

以這部蘭嶼的夕陽縮時來看，22 秒影片，用 ProRes 做 Codec 出來是 2.13 GB，用 H.264 的只有 171.7 MB

差了快 13 倍... 慘 ＝＝＋

<iframe width="560" height="315" src='https://www.youtube.com/embed/yBYp1rHxT_Q' frameborder='0' allowfullscreen></iframe>

<br>

## 後記的後記

在嘗試解決問題的過程中，我還曾尋求 ffmpeg 的幫助

結果雖然沒啥用，但卻也意外發現，原來 Codec 和 Container 似乎是兩回事呀！

ProRes 和 H.264 都屬於 Codec，.mov 和 .mp4 則屬於 Container

也就是說，不管你是用 ProRes 還是 H.264 做 Codec，都是可以輸出 .mov 或 .mp4，而不是像我原本以為 H.264 就只能輸出 .mp4 這樣的

啊～～ 不過 Codec 背後的原理我還是一點都不懂呀（倒）

而且這又讓人想起了當年數電實驗那崩潰的錄音機實驗（茶）

<br>

## 後記的後記的後記

現在想想，其實當初我在 Premiere 裡面做縮時的時候是把 Preset 做成 4k 而不是 4000 x 3000 的呀...

真不曉得換到 FCP 後自己幹嘛雞猴衝康自己 :p

<br>
