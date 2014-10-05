---
layout: post
---

用 AngularJS 搭配 HTML input 在 client side (browser) 上做相片的 exif parsing
---

<br>

之前曾經寫過一篇，在 server side 的 Node.js 上用 exiftool 來做相片的 exif parsing

而現在，因為我想讓 user 能夠從 browser 就直接上傳照片，所以才又有了必須在 client side 做 exif parsing 的需求

<br>

這篇的內容主要分成兩部分

1. 用 AngularJS 搭配 HTML input 來得到 user 上傳的 file
1. 使用 [exif-js][] library 來得到 file 的 exif

<br>

AngularJS + input 
---

HTML 的 input tag 很方便，可以直接幫我們做到讓 user 選取多個 file 的功能

但當 user 選完 files 後，該怎麼在 AngularJS 裡面拿到這些 files 呢？

經過 survey 後，我想主要有兩種方法能做到：

1. 直接把 input 的 onchange function 和 AngularJS 裡的 function link 起來
1. 寫一個 custom AngularJS directive，並在裡面用 element.bind('change') 的方式去聽 onchange

第二種方法比較複雜一點，但應該能讓 code 更 modularized，所以未來得再研究

第一種方法算最直接單純，直接在 html 中這樣寫

{% highlight html %}
input(id='file', type='file', accept='image/*', multiple, onchange='angular.element(this).scope().fileChanged(this)')
{% endhighlight %}

再到 AngularJS 中這樣寫

{% highlight js %}
$scope.fileChanged = function(e, $scope) {
	var file = e.files[0];
}
{% endhighlight %}

就能從 element.files 中拿到 user 透過 input 所選擇的 files 囉！

<br>

exif parsing by [exif-js][] library
---

Flickr 這篇文章寫的很棒，把整個在 client side 用 javascript 做 exif parsing 的原理和做法都講得清清楚楚

[Parsing Exif client-side using JavaScript][flickr]

原本是打算閱讀完並實作出來的啦，想說當作練功

但結果又不小心發現 bower 上已經有人做出 .js 了，所以就～～  ＸＤ（明明是自己太懶又太弱一下子不知道該怎寫）

雖然這個 library 目前還沒有 README，但看一下 example 後就會發現十分簡單好用

例如，只要這樣在拿到 file 後這樣做

{% highlight js %}
EXIF.getData(file, function(){
    alert(EXIF.pretty(this));
});
{% endhighlight %}

所有 exif 的資訊就會在 this 裡面啦！

<br>

最後，附上個小 Demo！

<p data-height="400" data-theme-id="0" data-slug-hash="AEBau" data-default-tab="result" data-user="namejoshua" class='codepen'>See the Pen <a href='http://codepen.io/namejoshua/pen/AEBau/'>AngularJS + <input> + exif-js demo</a> by yes (<a href='http://codepen.io/namejoshua'>@namejoshua</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//codepen.io/assets/embed/ei.js"></script>

<br>

[flickr]: http://code.flickr.net/2012/06/01/parsing-exif-client-side-using-javascript-2/
[exif-js]: https://github.com/jseidelin/exif-js