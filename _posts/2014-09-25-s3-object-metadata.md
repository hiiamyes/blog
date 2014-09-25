---
layout: post
---

在 S3 Object 的 Metadata 裡儲存中文！
---

AWS S3 的儲存方式，是必須先開個類似資料夾概念的 Bucket，然後再把檔案以 Object 的形式上傳進 Bucket 中

而在 Object 的幾項 Property 中，有一個叫做 Metadata 的東西

<img src="{{site.url}}/img/2014-09-25-s3-object-metadata/metadata.jpg" width="70%">

它是我打算用來存放照片的部分資訊，例如：date, keywords, ... 的地方

這樣一來，每當有需要修改這些資訊時，或許就可以透過只修改 Metadata 的方式

來大幅減少原本需要下載原始檔案做修改，然後再上傳回 S3 時所會產生的頻寬消耗

<br>

好啦
---

於是我開始嘗試著像這樣把照片連著 keywords 一起上傳

{% highlight js %}
s3.putObject({
	Bucket: 'bucketName',
	Key: 'keyName',
    Body: imageData,
    ContentType: 'image/jpeg',
    Metadata: {	keywords: '哈哈' }
}, function(err, data) {
    if (err) console.log(err);
    console.log('photo uploaded');
});
{% endhighlight %}

結果

<img src="{{site.url}}/img/2014-09-25-s3-object-metadata/error.png" width="100%">

error =..= 

這... 查了查後發現，應該是因為 Metadata 的 Value 不能吃中文吧？不過我沒有非常確定就是＠＠

[...Amazon S3 stores user-defined metadata in lowercase. Each name, value pair must conform to US-ASCII when using REST and UTF-8 when using SOAP or browser-based uploads via POST...][metadata]

<br>

但不管！我現在就是得解決這問題！
---

反正只要把中文變成英文加數字的組合就好了嘛（加密？），於是乎，我依序嘗試了三種方法

1. 用 [.charCodeAt()][charcodeat] 搭配 for-loop：	理論上可行，但稍微試過後就會知道這方法有多麼的愚蠢

1. 用 [utf8 - npm][utf8]：搜尋到的一個 module，理論上也是要可以用才對，但 .encode() 出來的 String 好像怪怪的，所以我暫時放棄

1. 用 Node.js 本身的 [Buffer][buffer]：最後使用的方法！


感謝這篇 stackoverflow [How to do Base64 encoding in node.js? - Stack Overflow][buffer-stack]

最後我就是以 Answer 中的方式來把中文的 keywords 做 encode，再上傳 S3，當然在下載 Metadata 後也得做相對應的 decode 這樣

{% highlight js %}
// encode
var keywords = new Buffer(keywords).toString('base64'),
// decode
var keywords = new Buffer(keywords, 'base64').toString();
{% endhighlight %}

<br>

後記
---

雖然暫時性地解決了問題，但其實我還是沒有完全了解 Unicode, UTF-8, ASCII, Base64 這些和編碼相關的技術之間的關係，以及原理是什麼

總覺得有點不踏實ＸＤ

<br>

[metadata]:http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingMetadata.html
[charcodeat]:http://www.w3schools.com/jsref/jsref_charcodeat.asp
[utf8]:https://github.com/nfroidure/UTF8.js
[buffer]:http://nodejs.org/api/buffer.html
[buffer-stack]:http://stackoverflow.com/questions/6182315/how-to-do-base64-encoding-in-node-js
