
# Using exiftool instead of imageMagick to manage metadata of photo by Node.js

之前會選擇用 im. (imageMagick) 而不是 exiftool，最大的原因是當初覺得 npm 上沒有 exiftool，所以可能會不好用，殊不知，im. 在 read metadata 時還算堪用，但當要 write metadata 時根本超級麻煩（也有可能單純是我不會用？），anyway，總之，我想通了，im. 還是應該用在它擅長的地方就好（影像處理），如果要 read / write metadata，我還是回頭來使用 exiftool 吧。

**但在 npm 上沒有 exiftool 該怎麼辦呢？**

**沒關係，nodejs 還有 child_process = =+**

簡單來說，就是在電腦上直接裝 exiftool，接著再用 child_process 直接開 thread 去執行 exiftool，得到的結果會再吐回 nodejs 裡的 callback，就這樣，實際使用過後發現以前寫的 im. code 真的都可以 delete 了。 

Orz...






