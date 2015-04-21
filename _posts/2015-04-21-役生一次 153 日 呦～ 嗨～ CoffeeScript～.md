---
layout: post
---

役生一次 153 日 呦～ 嗨～ CoffeeScript～
---

<br>

最近因為持續在寫山屋查詢網站的關係，所以終於又恢復了點 web development 的手感！（明明就還是個肉腳說什麼手感ＸＤ）

加上剛好有要 refactor 一份 .js code，所以打鐵趁熱，決定 '再來' 嘗試一次 CoffeeScript 啦！

<br>

恩...

再來？

<br>

哈哈，是因為在之前練習寫網站的過程中，我就已經學會用 Jade 寫 HTML，和用 Sass + Compass 寫 CSS 了

想當然爾，會繼續想練習用 CoffeeScript 寫 JavaScript 也是一件很合理的事嘛（茶）

But

不知道為啥，我記得好像嘗試了兩三次吧，最後都以失敗收場（遠目）

不是覺得不知道該怎麼 compile 好煩

就是覺得 aQ_QFunction = (hi) -> console.log 'Q_q' 這到底是什麼鬼啊根本看不懂

哈哈

<br>

還好現在變強終於看得懂了（挺？）

<br>

---

<br>

簡言之，要學會使用 CoffeeScript，必須經過三道關卡：

1. 安裝
2. Compile & Run
3. 寫 code ～～～

恩恩

<br>

---

<br>

## 安裝

十分 easy

* npm install -g coffee-script *

完成

（我以前都只做到這步就停了ＸＤＤＤ）

<br>

---

<br>

## Compile & Run

假設你有一個 yaya.coffee 內容是 `alert 'yaya'`

只要在 cmd 裡面打

* coffee -w -c yaya.coffee *

你就能每修改一次 yaya.coffee，就獲得一份新的 yaya.js 啦

接著再

* node yaya.js *

恩～ 一切都是多麽的美好～～

（我也不懂為啥以前都不知道該怎麼在 cmd 裡面做這些事 ＝～＝）

<br>

---

<br>

## 寫 code ～～～

前面說過，我已經在使用 Jade 寫 HTML，用 Sass + Compass 寫 CSS 了

但其實，圖的也就只是不用寫些 ; {} <> () 等等的而已啦

CoffeeScript 當然也能做到這些，但麻煩(?)的就是，它還能做到更多...（倒）

（不過平心而論，這也很正常啦，畢竟本質上是要寫 Javascript 啊，當然和 HTML CSS 差一大截ＸＤ）

* 不用再寫 ;
* 不用再寫 var
* 不用再寫一堆 {} () [] 

以上是基本款，所以不貼 code 啦～

以下，則是終於在今天學會了的神奇 CS 語法們～～

<br>

* 煞氣Ａ方勳： (A_A) -> A_A

Before Compilation

<img src="{{site.url}}/img/2015-04-21/before.png" width="60%">

After Compilation

<img src="{{site.url}}/img/2015-04-21/after.png" width="60%">

（後來寫到一半才發現... 竟然 call function 時的小括號有時候也可以不用寫... 所以上面的 code 還不是最精實的 ＝,.＝）

<br>

還有還有

* 變超簡單好用的 switch、for、if 

* 以及很誇張地從符號變成白話文的 comparator

{% highlight js %}
// Need some days to make up the 1st week if the 1st staus if not Sunday.
if (i == 0 && day != 0) {
    for (var dayIndex = 0; dayIndex < day; dayIndex++) {
        hutApplicableInOneWeek.push({});
    };
};
{% endhighlight %}

{% highlight coffee %}
# Need some days to make up the 1st week if the 1st staus if not Sunday.
if istatus is 0 and day isnt 0
    hutApplicableInOneWeek.push {} for [0...day]
{% endhighlight %}

<br>

---

<br>

呼～

總之～

今天總算是又完成了一個想了好久的目標ＸＤ

就是用 CS 讓 code 變得超乾淨的啦～～～ 

（恩... 但看看下面這 refactor 後的 code... 怎麼好像... 有點變的更難看懂了啊...（誤））

<img src="{{site.url}}/img/2015-04-21/final.png" width="80%">

<br>
