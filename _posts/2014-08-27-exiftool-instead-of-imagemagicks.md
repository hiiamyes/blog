
# Using exiftool instead of imageMagick

# For managing metadata of photo by Node.js

之前會選擇用 im. (imageMagick) 而不是 exiftool，最大的原因是當初覺得 npm 上沒有 exiftool，所以可能會不好用，殊不知，im. 在 read metadata 時還算堪用，但當要 write metadata 時根本超級麻煩（也有可能單純是我不會用？），anyway，總之，我想通了，im. 還是應該用在它擅長的地方就好（影像處理），如果要 read / write metadata，我還是回頭來使用 exiftool 吧。

**但在 npm 上沒有 exiftool 該怎麼辦呢？**

**沒關係，nodejs 還有 child_process = =+**

簡單來說，就是在電腦上直接裝 exiftool，接著再用 child_process 直接開 thread 去執行 exiftool，得到的結果會再吐回 nodejs 裡的 callback，就這樣，實際使用過後發現以前寫的 im. code 真的都可以 delete 了。 

Orz...

---

以下是一點 coding 記錄：

####install exiftool
```sh
brew install exiftool
```

####usage
```nodejs
var cp = require('child_process');
// show keywords of photo
cp.exec('exiftool -keywords photo.jpg', function(err, stdout, stderr) {
    console.log(stdout);
});

```
上面 -keywords 的部分，還可以替換成
* -keywords+={travel,coding} ：把 keywords 增加 travel 和 coding
* -gps* ：把 gps 開頭的 metadata 都列出來
* -gpslatitude=25.1111 

---

大致上就是這樣囉，謝謝～！


reference:
---
[ExifTool]
[child_process] 


[exiftool]:http://www.sno.phy.queensu.ca/~phil/exiftool/
[child_process]:http://nodejs.org/api/child_process.html





