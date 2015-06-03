---
layout: post
---

役生一次 196 日 Visualization + D3.js - Part 1
---

<br>

網站寫了一陣子，也開始碰到 UI 上的瓶頸了，尤其是像這種資料呈現類的網站，特別需要對資料做視覺化的設計

例如，把剩餘山屋床位的數量做成長條圖，應該就會是個不錯的嘗試和練習

<img src="{{site.url}}/img/2015-06-03/hut.png" width="60%">

<br><br>

早就聽說 D3.js 很久了，於是決定利用這個機會開始學一下！ 不過這篇還不會碰到關於繪圖的部分，只是先簡單玩個 Hello World 就好 ＸＤ

D3 是 Data-Driven Documents 的縮寫，實際摸過後就會發現，它其實就是個幫你封裝了許多資料處理、DOM 操作等等 javascript function 的 library

以我自己的意思來說，它其實就像個繪圖版的 jQuery 啦

<br><br>

來吧，D3.js + Hello World

<script src="https://gist.github.com/hiiamyes/126f79fbe194f7d1d40e.js"></script>

這段簡單的 code 是在讀過 Scott Murray 所寫的 [Tutorial](http://alignedleft.com/tutorials/d3/using-your-data) 後寫出來的

HTML 的部分就不說明了

Javascript 的部份說明如下

* .selectAll 'p'：這個很有特別，哈，要配合 .data 一起看

* .data：會把定義好的 data array 讀進去，例如這邊的 data array 有 10 個 char，那 .data 就會配合上面的 .select 和 .selectAll 創造出 10 個 placeholder (不是 p 喔) 在 body 裡面，超神奇！（其實這點說得不算完全正確，請看下一項ＸＤ）

* .enter：上面所說的 10 個 placeholder 的創造，其實應該是靠 .enter 這個 function 啦

* .append：因為上面只創造出了 10 個 placeholder，還沒有任何內容，所以要再把 p 這個 HTML tag append 上去

* .text：最後用 .text 把 data 餵給 p 吃，這邊寫得很簡陋，哈，其實就是丟給 .text 一個 function，而這個 function 會有一個參數 d，也就是我們用 .data 所吃進來的 data (這也是 D3 很神奇的一個東西！)，然後把 d return，自然 text 就會拿到 hello world 的 char 啦！

* 最後，非常需要一提的是，若你想把 D3 相關的 js code 獨立出來的話，記得 script reference 要寫在 body 裡面喔，寫在 head 裡面的話可是會失敗的（攤手）

<br><br>

OK，結果如下

<img src="{{site.url}}/img/2015-06-03/d3.png" height="600px">

<br>