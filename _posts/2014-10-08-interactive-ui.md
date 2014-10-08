---
layout: post
---

用 AngularJS + Pseudo Class 來做 Interactive UI
---

<br>

<p data-height="400" data-theme-id="0" data-slug-hash="blrqH" data-default-tab="result" data-user="namejoshua" class='codepen'>See the Pen <a href='http://codepen.io/namejoshua/pen/blrqH/'>basic interactive icon</a> by yes (<a href='http://codepen.io/namejoshua'>@namejoshua</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

<br>

猶記得當年，第一次發現原來 Android 裡面有個 [StateListDrawable][selector] 可以輕易地幫我們做出 Interactive UI 時，超訝異又興奮的

花了不少時間周旋在 state_pressed, state_selected, ... 等等等當中，覺得做 UI 的功力好像提升了一個檔次

從此以後，每當看到任何一個 Button，總是會去戳戳它看看會不會有不同 State 的相應變化（職業病養成！）ＸＤ 

<br>

### 這樣的好習慣（？），當然在跑來 Web 開發後也得繼續保持呀！

<br>

經過了一陣子 Web 開發的基礎練習後，我發現

***在 Web 的世界裡要做到 UI 的動態變化，很基本的一個方式就是利用 Add/Remove Class + CSS 的方式來達成***

[pseudo-classes][] 大概就是在這樣的想法下，被製造出來的一種便利工具吧

也就是說，[pseudo-classes][] 幫我們處理了許多常見的 Add/Remove Class 的部分，讓我們只需要寫相對應的 CSS 就好

例如在上方的 Demo 中，我們能夠很輕易地利用

* :hover，定義出 UI 在 MouseOver 狀態下的 UI 變化
* :active，定義出 UI 在 MousePressed 狀態下的 UI 變化

<br>

### 當然，有些還是得自己來做啦～ 例如 select 狀態

<br>

select 狀態在 Android 裡面也一樣沒那麼能直接做到，哈，畢竟 select 在本質上是需要一點 data binding 的

也就是說，我至少得有個 data，來記錄 isSelected = true or false

然後，再根據 isSelected 來做 Add/Remove Class + CSS 的部分

當然 CSS 的部分完全不是問題，稍微麻煩的是 Add/Remove Class 的部分

傳統上應該是會使用 jQuery，來在 Event Listener 裡面完成任務

不過，今天我使用的是 AngularJS，所以事情稍微簡單了點，我只要把以下兩部分

* `ng-class="{select:isSelected}"`（如果 `isSelected = true`，則加入 `class 'select'`，若否則清掉 `class 'select'`）
* `ng-click="isSelected=!isSelected"`

加入 HTML 中的任意一個 Tag 裡，就能讓那個 Tag 擁有 Click for Selection 的功能啦！！！

當然當然，這部分啊其實，應該可以再偷偷做成 Custom Directive 讓它更漂亮的ＸＤ

<br>

[selector]: http://developer.android.com/guide/topics/resources/drawable-resource.html
[pseudo-classes]: https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes