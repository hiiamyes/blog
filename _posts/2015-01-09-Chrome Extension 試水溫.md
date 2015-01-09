---
layout: post
---

Chrome Extension 試水溫
---

<br>

一直都想做個那種，反白網頁上看到的英文單字後，會自動幫你查好並呈現出來的小工具，當然，這功能已經有很多 Extension 做了啦

不過，一來是因為，我還想要這工具能有更多功能，二來是，我想透過寫 Extension 的過程練習網站三寶（HTML, CSS, Javascript）

所以，就決定利用幾天時間，來自己刻出個查字典 Extension，的雛形！

---

<br>

第一步，當然還是 Hello World，照著 [Tutorial][] 走，一切十分 easy 美好～

只要一個 manifest.json、一張 icon.png、再一個 popup.html，完成～

manifest.json
{% highlight json %}
{
    "manifest_version": 2,

    "name": "YesDic",
    "description": "Dic by Yes!",
    "version": "0.0",

    "browser_action": {
        "default_icon": "icon.png",
        "default_popup": "popup.html"
    },
}
{% endhighlight %}

popup.html
{% highlight html %}
<!doctype html>
<html>
<body>
hallo world!
</body>
</html>
{% endhighlight %}

<img src="{{site.url}}/img/2015-01-09/yesdic/hello.png" height="150px">

恩～ 不過就是因為這一步太 easy 了（基本的有點過頭＝＝a...），反而讓我一下子不知道下一步想要做的事情該往哪個方向找資料

喔對，下一步我要做的，就是如何去抓到 **使用者把文字反白了** 這件事

好的，所以現在只好先看看文件，了解一下 Extension 的 Project 有哪些特色啦

邊看邊整理的內容如下：

* Action：分成 Page Action 和 Browser Action，這部分沒什麼用

* chrome.* 開頭的特殊 API：這部份也還不知道會不會用到

* Background Page：又分成永久存在的 Persistent Background Page，以及需要時才存在的 Event Page

* UI Page：大概就是可以用 HTML 做出 UI 吧，我還不太需要

* Content Script：...some JavaScript that executes in the context of a page that's been loaded into the browser.

喔喔喔，看來我要抓到使用者做的 **反白** 動作，就是得靠 Content Script 啦！

manifest.json
{% highlight json %}
{
    "manifest_version": 2,

    "name": "YesDic",
    "description": "Dic by Yes!",
    "version": "0.0",

    "browser_action": {
        "default_icon": "icon.png",
        "default_popup": "popup.html"
    },

    "content_scripts": [{
    	"matches": ["<all_urls>"],
    	"js": ["content_script.js"]
	}]
}
{% endhighlight	%}

<br><br><br><br>

### 恩，不過問題來了，反白的 event... 是什麼＝＝？

這東西一開始還真是超難搜尋的，因為不知道關鍵字該下什麼，搞了半天才知道原來是，select 

不過同時也發現，HTML DOM 的 event 中根本沒有提供什麼 onSelect 之類的 API ＝＝＋

這...（翻桌～～～）

還好聰明如我，終於在苦苦 google 了良久後，發現原來可以這麼做呀...

{% highlight js %}
window.onmouseup = function() {
    var word = window.getSelection().toString();
}
{% endhighlight %}

登登～～

拿到了 User 反白的 String 後，下一步當然就是

<br><br><br><br>

### 查 字 典

平常用的都是 yahoo 字典，雖然他沒有提供 API，不過，URL，像這樣 

https://tw.dictionary.yahoo.com/dictionary?p=hello

說明了一切（笑）

用 HTTP Request 去戳吧！

之前寫 Javascript 時，都是用 AngularJS 包好的 $http 來做 request 的

但這次我不知道該怎麼在寫 Extension 的時候使用 AngularJS，當然也不想花時間去研究了

索性就當成個練習寫 Pure Javascript 的機會！

#### 用 XMLHttpRequest 戳 yahoo 字典

基於以前的經驗，我本來想說 XMLHttpRequest 應該會回給我 text response，所以我得再想辦法 parse 成 HTML 的樣子

於是就找到了個 DOMParser 要來做這件事

{% highlight js%}
var xhttp = new XMLHttpRequest();
var parser = new DOMParser();
xhttp.onload = function() {
	var doc = parser.parseFromString(this.response, "application/xml");
};
xhttp.open("get", "https://tw.dictionary.yahoo.com/dictionary?p=hello", true);
xhttp.send();
{% endhighlight	%}

結果...

<img src="{{site.url}}/img/2015-01-09/yesdic/err2.png" width="100%">

<img src="{{site.url}}/img/2015-01-09/yesdic/err1.png" width="100%">

好像 parse 失敗...（抓頭）

不過在找到 error 的原因前，我就先發現 XMLHttpRequest 原來有個 responseType 可以設定呀

因此只多加了一行，就不用自己做 parse 啦～～

{% highlight js%}
var xhttp = new XMLHttpRequest();
xhttp.responseType = "document";
xhttp.onload = function() {
    var elements = this.response.getElementsByClassName("explanation");
    var result = elements[0].innerText;
};
xhttp.open("get", "https://tw.dictionary.yahoo.com/dictionary?p=hello", true);
xhttp.send();
{% endhighlight	%}

最後，再順便研究吐回來的 document，我決定先把 class = explanation 的第一個拿出來當 result

<img src="{{site.url}}/img/2015-01-09/yesdic/http.png" height="200px">

OK，HTTP Request 的部分做完了，終於剩下

<br><br><br><br>

### UI... （累）

覺得累，所以直接用 code 代替文字吧，反正這 UI 根本世界無敵醜陋ＸＤ

簡單說就是塞塊 id = result 的 div 到網頁裡，然後把他的 innerText 改成查字典查到的結果而已～

content_script.js

{% highlight js %}
var newdiv = document.createElement('div');
newdiv.setAttribute('id', 'result');
newdiv.setAttribute('style', 'position:fixed; bottom:0px; right:0px; width:200px; height:200px; background-color:red;');
document.body.appendChild(newdiv)
var element = document.getElementById('result');

window.onmouseup = function() {
    var word = window.getSelection().toString();
    if (word != "") {
        var xhttp = new XMLHttpRequest();
		xhttp.responseType = "document";
		xhttp.onload = function() {
    		var elements = this.response.getElementsByClassName("explanation");
    		var result = elements[0].innerText;    		
            element.innerText = result;
		};
		xhttp.open("get", "https://tw.dictionary.yahoo.com/dictionary?p=hello", true);
		xhttp.send();
    };
}
{% endhighlight %}

<img src="{{site.url}}/img/2015-01-09/yesdic/ui.png" height="200px">

<br><br><br><br>

### 好，付了 5 美金，上架囉～～～～～  終於～～ Ｔ＾Ｔ

<img src="{{site.url}}/img/2015-01-09/yesdic/store.png" height="200px">

開熏～ 立馬試用看看～～～

<img src="{{site.url}}/img/2015-01-09/yesdic/err3.png" width="100%">

乾...

<img src="{{site.url}}/img/2015-01-09/yesdic/ggonline.png" height="200px">



<br><br><br><br>

### 有 Bug 就要 Debug（廢話？）

什麼奇怪的 HTTP HTTPS 問題我搞不懂啦 Ｑ＿Ｑ

儘管如此，還是靠著強大的 Stack Overflow

1. 把 Content Script 裡面 HTTP Request 的部分搬到 Event Page 裡

2. 透過 [Messaging][] 的方式讓 Content Script 叫 Event Page 戳 yahoo，再將結果 pass 回 Content Script 然後 display 在 div 裡

manifest.json
{% highlight json %}
{
    "manifest_version": 2,

    "name": "YesDic",
    "description": "Dic by Yes!",
    "version": "0.0",

    "browser_action": {
        "default_icon": "icon.png",
        "default_popup": "popup.html"
    },

    "background": {
        "scripts": ["eventPage.js"],
        "persistent": false
    },

    "content_scripts": [{
    	"matches": ["<all_urls>"],
    	"js": ["content_script.js"]
	}]
}
{% endhighlight	%}

content_script.js
{% highlight js %}
window.onmouseup = function() {
    var word = window.getSelection().toString();
    if (word != "") {
        chrome.runtime.sendMessage({
            data: word
        }, function(result) {
            var element = document.getElementById('result');
            element.innerText = result;
        });
    };
}
{% endhighlight %}

eventPage.js
{% highlight js %}
chrome.runtime.onMessage.addListener(function(request, sender, callback) {
    var xhttp = new XMLHttpRequest();
    xhttp.responseType = "document";
    xhttp.onload = function() {
        var elements = this.response.getElementsByClassName("explanation");
        var result = elements[0].innerText;
        callback(result);
    };
    xhttp.open("get", "https://tw.dictionary.yahoo.com/dictionary?p=" + request.data, true);
    xhttp.send();
    return true; // prevents the callback from being called too early on return
});
{% endhighlight %}

好啦，結果

<iframe src="{{site.url}}/img/2015-01-09/yesdic/yaya.mp4" width="640px" height="400px"></iframe>	

<br><br><br>

＾＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＾

[Messaging]: https://developer.chrome.com/extensions/messaging
[Tutorial]: https://developer.chrome.com/extensions/getstarted

<br>
