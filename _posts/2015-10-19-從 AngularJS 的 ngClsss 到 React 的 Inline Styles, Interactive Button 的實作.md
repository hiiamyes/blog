---
layout: post
---

從 AngularJS 的 [ngClsss][ng-class] 到 React 的 [Inline Styles][inline-styles] - Interactive Button 的實作
---

<br>

身為一位 Frontend Developer，常常考慮著 Interactive Design 也是一件很合理的事嘛～

而最常見的例子，就是按下一個 button 後，button 的樣子必須要有所改變這件事呀～！

<br>

剛開始接觸 Web Development 的時候我是選用 AngularJS 的

在 AngularJS 裡，我可以透過 ngClass 和 ngClick 的搭配，去動態增加一個 .click 的 class 給 button

最後再配合 CSS，就能完成 Interactive Button 的效果啦

這樣的方法，其實寫起來的感覺和利用 jQuery 增減 element 的 class 並搭配 CSS 的做法十分類似

<p data-height="268" data-theme-id="20155" data-slug-hash="epeaja" data-default-tab="result" data-user="namejoshua" class='codepen'>See the Pen <a href='http://codepen.io/namejoshua/pen/epeaja/'>Interactive Button with AngularJS's ngClass</a> by yes (<a href='http://codepen.io/namejoshua'>@namejoshua</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>
 
<br><br><br>

恩～ 不過今天換到了 React 上，可就沒有類似 ngClass 的東西了（攤手），不過卻也多了個 Inline Style 可以用！

React 的 Inline Style，使用的是我以前完全沒想過，也沒聽說過的 CSS in JS 概念

這篇 Slide「[React: CSS in JS][css-in-js]」非常清楚地說明了一切，有興趣的請自行閱讀

而下面，我只想用 code 和 demo 來說話，並做一點點簡單的說明ＸＤ

<br>

其實從 code 來看，CSS in JS 的使用方式，倒也是很好理解的

首先，我們把原本寫在 CSS 裡的東西，改寫成一個 Object Variable 並放在 React Component 裡

接著，把控制 button 狀態的變數（在 demo 裡面指的就是 isClick），寫成 Component 的 State，並加上一個 onClick Event

最後，再給 button 一個名為 style 的 attr，並把 state、css rule 和一些判斷式加入

登登～ React 版的 Interactive Button 就出現啦

<p data-height="777" data-theme-id="20155" data-slug-hash="xwPNmw" data-default-tab="result" data-user="namejoshua" class='codepen'>See the Pen <a href='http://codepen.io/namejoshua/pen/xwPNmw/'>Interactive Button with React's Inline Styles</a> by yes (<a href='http://codepen.io/namejoshua'>@namejoshua</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

<br>

恩，至於，在有了 Inline Style 後，以後我們是不是就該把所有的 CSS 都寫到 JS 裡勒？

阿～ 這就又是另外一個故事啦～ （茶）

<br><br>

[ng-class]: https://docs.angularjs.org/api/ng/directive/ngClass
[inline-styles]: https://facebook.github.io/react/tips/inline-styles.html
[css-in-js]: https://speakerdeck.com/vjeux/react-css-in-js
