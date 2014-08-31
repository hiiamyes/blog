用 Node.js + AWS SDK 操作 s3
---

要操作 s3 應該有三種方法：

1. 用 AWS CLI
1. 用 AWS SDK for different languages, like JS, Ruby, ...
1. 用 REST API call 

用 CLI 的方式之前玩過了，所以今天要再來試用 SDK 的方法，而使用的語言就是 Node.js！

下面要進行的步驟有幾個：
---
1. set and load config.json
2. create / delete Bucket
3. upload / list / delete / download Photo (Object)

幾乎全部的內容都可以在

* [AWS SDK for JavaScript in Node.js][aws-sdk] 
* [API Documentation][aws-sdk-api] 

找到

Config.json
---
首先，要讓你的 code 有權限 access s3 server，你必須做兩件事

1. 到 IAM 建立個 User 並 ***打開適當的權限*** （在 CLI 的時候做過囉就不再說明）
2. create a config.json 並在 code 裡面 load 它（在 SDK 的 getting started 裡面就有囉就不說明） 

於是我們可以在 code 的開頭部分寫上

    var aws = require('aws-sdk');
	aws.config.loadFromPath('config.json');
	var s3 = new aws.S3();

接下來就可以用這個 var s3 對 server 做各種操作！

Bucket
---
create 和 delete Bucket 要成功很簡單

只要給個 Bucket 的名字再 call call API 就好了

{% highlight JavaScript %}
    function createBucket() {
    	var params = {Bucket: 'hiiamyestestbbb'};
    	s3.createBucket(params, function(err, data) {
    		if (err) throw err;
          	console.log('bucket created');
        });
    }       

    function deleteBucket(){
		var params = {Bucket: 'hiiamyestestbbb'};
    	s3.deleteBucket(params, function(err, data){
			if (err) throw err;
			console.log('bucket deleted);
		});
	}
{% endhighlight %}

完成～

不過真正複雜的是在理解 api document 裡那一卡車 params 吧，留待以後囉


Object
---
Object 的操作在這邊我用照片當例子

首先，list object 和 delete object 都很簡單，都是直接使用 API `s3.listObjects()` `s3.deleteObject()` 就好

而 upload 和 download 稍微複雜點，因為使用上得搭配 fs

    function uploadPhoto() {
        fs.readFile('photo.JPG', function(err, data) {
            var params = {
                Bucket: 'hiiamyestestbbb',
                Key: 'photo1.jpg',
                Body: data,
                ContentType: 'image/jpeg'
            };
            s3.putObject(params, function(err, data) {
                if (err) throw err;
                console.log('photo uploaded');             
            });
        });
    }

特別要注意的就是 params 裡面的 Body 和 ContentType 該如何設定吧

（其實 permission 應該也是要一起設定的，但我懶得練習了，以後再說ＸＤ）

    function downloadPhoto(){
        var params = {
            Bucket: 'hiiamyestestbbb',
            Key: 'photo1.jpg'
        }
        s3.getObject(params, function(err, data){
            if(err) throw err;
            fs.writeFile('savedPhoto.jpg', data.Body, function(err){
                if(err) throw err;
                console.log('photo saved');
            });
        });
    }

download 的部分則必須特別注意，回來的 data 裡面可不只有 object data 喔！ 

所以得去看看 [API Documentation][aws-sdk-api]，然後才知道 object data 是放在 data.Body 裡面的

最後再用 fs 把它存成 .jpg 就完成啦！

<img src="{{site.url}}/img/2014-08-31/folder.png">

後記
---

npm 上當然也有人做出了方便使用的 package [npm-s3] 

但在使用 pakcge 前，我還是習慣自己用最基本的 code 簡單 implement 一下

除了比較踏實外，之後要去看 package 的 source code 也會比較輕鬆！


[npm-s3]: https://www.npmjs.org/package/s3
[aws-sdk]: http://aws.amazon.com/sdk-for-node-js/
[aws-sdk-api]: http://docs.aws.amazon.com/AWSJavaScriptSDK/latest/frames.html