---
layout: post
---

用 ES6 改寫原本用 CoffeeScript 寫的 React Component
---

<br>

先說說成功完成了 Refactoring 的感想... 

真的是好痛苦呀～（眼神死）

<br>

前一陣子把[「山上天氣怎麼樣」][web]網站的雛形給寫了出來，但是是用已經習慣了的 CoffeeScript 寫的

有鑒於未來百分之百會改用 ES6，因此決定在繼續往下寫之前，著手先進行一次 Refactoring

<br>

左邊是用 CoffeeScript 寫的 React Component，右邊是用 ES6 重新寫過的

這樣比較對照，應該就能明顯地看出兩種寫法不同的地方

<style type="text/css"> 
	.gist {width:45%; display: inline-block; vertical-align: top;}  
</style>

<script src="https://gist.github.com/hiiamyes/6670d0b6b756074e9ef1.js?file=app.cjsx"></script>

<script src="https://gist.github.com/hiiamyes/6670d0b6b756074e9ef1.js?file=app.js"></script>

這邊記錄下幾個重點：

1. Module 的 Loading 從使用 require 改成使用 ES6 的 Module System，所以改用 import 來 load module

1. [ES6 Classes][es6-classes]: 從使用 React 提供的 createClass API，改成使用 ES6 的 Class 宣告方式來產生 React Component 

1. 不再需要 getInitialState 來初始化 props 和 state 了，改成在 ES6 class 的 constructor 裡進行

1. [No Autobinding][no-autobinding]: function 不再會自動把 this bind 進來了，所以 mountainClick() function 必須先在 constructor 裡做一個 bind this 的動作，才能夠拿到 this.state

1. 變數宣告要記得加 var，該寫的括號、逗號、分號不能少了...

恩，大致上就是這些

<br><br><br>

改完了 Component 的 code 後，當然，webpack 的設定也是得做點調整的

我是改用 [babel-loader][] 取代原本的 [coffee-jsx-loader][] ，並記得加入 [babel-preset-react][] 當作 preset，不然 loader 會認不出 JSX 喔！

<script src="https://gist.github.com/hiiamyes/6670d0b6b756074e9ef1.js?file=webpack.config.js"></script>

<br>

好了

輕描淡寫地記錄下 Refactoring 的結果，其實真正的目的是想刻下一條，自己曾經用過 CoffeeScript 的痕跡

啊，但寫不出的是過程中自己的弱小和無助就是～ Ｑ＿＿＿Ｑ

謝謝觀看，大家再見！

<br>

Ref: [Refactoring React Components to ES6 Classes][refactor]

<br><br>

[es6-classes]: https://facebook.github.io/react/docs/reusable-components.html#es6-classes
[no-autobinding]: https://facebook.github.io/react/docs/reusable-components.html#no-autobinding
[web]: https://www.youtube.com/watch?v=3Jl0tAJTJq4
[refactor]: http://www.newmediacampaigns.com/blog/refactoring-react-components-to-es6-classes
[coffee-jsx-loader]: https://github.com/jsifalda/coffee-jsx-loader
[babel-loader]: https://github.com/babel/babel-loader
[babel-preset-react]: https://github.com/babel/babel/tree/master/packages/babel-preset-react