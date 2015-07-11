---
layout: post
---

役生一次 233 日, 實作 Material Design 的 Sidenav (Web)
---

<br>

藉著這次台灣山屋餘額查詢網的更新，我再一次地練習到了 Web 的 Animation 操作

因為更新後圖表佔的空間會變大，所以我得把原本固定放在網頁上方的山屋清單，改藏到網頁左側的抽屜，也就是 Sidenav 裡

<img src="{{site.url}}/img/2015-07-10/before.png" width="45%">
<img src="{{site.url}}/img/2015-07-10/after.png" width="45%">

<br>

記得上次做 Animation 時是用 Keyframe 做的，但 Sidenav 因為只需要個單方向的 Translation 和 Opacity 改變，所以這次就不需要用到 Keyframe 了

不過由於我和 Material Design 很不熟，所以這次還先去看了 [Google 的 Demo][google-demo]

然後再到 Codepen 上找了份 Code 來當作參考 ([Off Canvas Menu][]) 來模仿 

<p data-height="600" data-theme-id="0" data-slug-hash="xbmevK" data-default-tab="result" data-user="matheusxaviersi" class='codepen'>See the Pen <a href='http://codepen.io/matheusxaviersi/pen/xbmevK/'>off canvas menu</a> by Matheus Silva (<a href='http://codepen.io/matheusxaviersi'>@matheusxaviersi</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

其中，利用 input 搭配 label 的方式來做到開關控制的效果這招滿帥的 ＸＤ

但因為一些原因，後來我並沒有採用，而是直接用 AngularJS 的 Scope Variable 開一個 Boolean 來當作開關

<br><br>

## Pseudo Code

<br>

### HTML 的部分

<script src="https://gist.github.com/hiiamyes/43790456ce1d37efebf8.js?file=index.jade"></script>

這邊只寫出網頁上所必需得三個東西

* 用來當抽屜的 Sidenav
* 用來放網頁內容的 Content
* 當作抽屜開關的 Toggle

接著再搭配 AngularJS 的 ng-class 和 ng-click，讓 Toggle 開關的時候可以把 .toggle 的 class 加上 Sidenav 和 Content

再搭配上 CSS，就能做到動態的 Attribute 改變

<br>

### CSS 部分

<script src="https://gist.github.com/hiiamyes/43790456ce1d37efebf8.js?file=index.sass"></script>

製作 Animation 最根本的邏輯、方法，就是設定好 Transition，然後透過 class 的變化去改變相對應的 Attribute

然後會受到 Transition 影響的 Attribute 就會產生 Animation 效果啦！

以 Sidenav 的部分來說，在 Toggle 狀態為關閉時，Opacity 會從 1 變成 0，所以就會產生 fadeout 的效果

而 Content 的部分，在 Toggle 狀態為開啟時，因為 translateX(22%) 的關係，就會有一個向右移動 22% 的 Animation 出現，也就是抽屜打開的效果！

<br>

### AngularJS 部分

<script src="https://gist.github.com/hiiamyes/43790456ce1d37efebf8.js?file=controller.coffee"></script>

最後，利用 AngularJS 的 ng-click 和 ng-class

我們可以很簡單的做到動態加入 class 的功能，開心ＸＤ

<br><br>

## Demo

我懶得錄只有 Sidenav 部分的 Demo 影片了

所以直接拿網站更新的 Demo 來充當一下吧 ＸＤ

請看 15 到 24 秒的部分～

<iframe width="640" height="360" src="http://www.youtube.com/embed/j9KsFYMCmgk?rel=0&start=15&end=24" frameborder="0" allowfullscreen></iframe>

<br>

[google-demo]: https://material.angularjs.org/latest/#/demo/material.components.sidenav
[Off Canvas Menu]: http://codepen.io/matheusxaviersi/pen/xbmevK?editors=110