---
layout: post
---

役生一次 214 日, 用 Electron 寫 Desktop App, Part 2
---

<br>

當了替代役，也不能忘記你原本是做什麼的

秉持著這個信念，我開始寫了個「東西」，至於這「東西」是什麼？ 恩，先等等，先讓我說說替代役平常在登山口的工作是怎麼一回事

在登山口，每天的工作其實非常單純，主要就分為兩部份而已

<br><br>

### 第一部分：文書作業

#### 1. 用官方帳號登入系統

<img src="{{site.url}}/img/2015-06-21/routine0.png" width="45%">
<img src="{{site.url}}/img/2015-06-21/routine1.png" width="45%">

<br>

#### 2. 下載登山名冊

<img src="{{site.url}}/img/2015-06-21/routine2.png" width="45%">
<img src="{{site.url}}/img/2015-06-21/routine3.png" width="45%">

<br>

#### 3. 用登山口的電腦再做成「另外一份」，用來記錄登山客上下山狀態用的「Local 端登山名冊」

<img src="{{site.url}}/img/2015-06-21/routine4.png" width="45%">
<img src="{{site.url}}/img/2015-06-21/routine5.png" width="45%">
<img src="{{site.url}}/img/2015-06-21/routine6.png" width="90%">

<br>

恩，就是個非常 routine 的動作而已，而通常，我們會一次做好未來 3 天左右的名冊這樣

<br><br><br>

好，接著

<br><br><br>

### 第二部分：登記作業

登記作業，顧名思義，就是當山友們經過登山口這邊要上山或下山時，我們都得在上面做的「Local 端登山名冊」中進行一個登記的動作

主要就是「用顏色註明各隊伍的上下山狀況」、「登記上下山實際時間」、「登記上下山實際人數」這樣

<img src="{{site.url}}/img/2015-06-21/routine7.png" width="50%">

<br><br><br>

### 好啦，身為一位工程師，在一個環境裡待久了，當然慢慢就會去找些雞毛蒜皮的問題出來 XD

1. 一直重複 routine 的動作超不符合工程師的哲學的！我要一個自動幫我更新登山名冊的工具啦！！！！

1. 網路上下載回來的登山名冊，無法確定它的更新日期是什麼時間點，所以有時候會有小小不同步的情況發生 (就是少隊伍或多隊伍或人數不對這樣)

1. 每次輸入隊伍上下山時間時都要手動打，好麻煩 (?)，所以很想要按個按鈕就能自動填入現在時間 :p

1. 因為 Local 端登山名冊是用上山時間做分類的，所以在隊伍下山需要登記時，還要去看隊伍是哪一天上山的再去搜尋這樣，頗麻煩 (當然也能直接 Ctrl+F 領隊名字啦)

1. Local 端登山名冊其實有太多不需要被顯示出來的欄位了

1. Local 端登山名冊沒有做雲端同步的動作，所以只能在登山口看，恩... 當有颱風來的時候...

1. 其實還有一個隱藏問題，想知道的可以私下偷偷問我 XD

恩，好的，所以

為了解決以上這些雞毛蒜皮的問題們，我決定來做個「東西」，那就是

<br>

**SHMS (Shei-Pa Hiker Management System)**

<br>

一來，就是希望能把太 routine 的工作用一個 Desktop App 自動化起來

二來，則是希望讓登山口的登記作業做起來能夠更簡便、有效率，並期望能得到更大的附加價值！ (非常冠冕堂皇)

<br><br><br><br><br>

恩，以上，終於說完了創作動機 (累)，後面終於要開始說明程式部分啦～～！

<br><br><br>

### 但其實最困難 (最白癡) 的中文字顯示問題已經在 Part 1 裡解決了，所以接下來其實只有簡述下程式架構而已 XD

目前程式的架構非常單純，大概就是 Electron + Crawler + AngularJS 而已

<br>

#### Electron 

的部分就不說了

<br>

#### Crawler 

因為前一陣子靠著爬山屋餘額已經練就出一番神功，所以實際上也是很快就寫出來了，很簡單地就是包含了

1. 登入帳號

1. 爬出資料

1. 以及一個編碼問題的小插曲 XD

<img src="{{site.url}}/img/2015-06-21/crawler1.png" width="45%">
<img src="{{site.url}}/img/2015-06-21/crawler2.png" width="45%">

<br>

#### AngularJS

再次覺得 AngularJS 太好用了，而且因為 Electron 能直接在 Render Process 裡面使用 Native Module

所以我可以直接把 Crawler 寫在 AngularJS 的 Controller 裡面，超～級～爽～ (當然這只是剛開始這樣寫啦，以後應該不可能寫在這裡面)

<img src="{{site.url}}/img/2015-06-21/angularjs.png" width="45%">
<img src="{{site.url}}/img/2015-06-21/html.png" width="45%">

<br>

#### 完成

這就是熱騰騰的 0.1 版啦，算是可以終於可以拿出個實物來和別人說明理念的程度了，但當然還有非常長的路要走 (茶)

接下來就是在退伍前持續努力了！希望真的有機會能成為個體制內的工具囉！ (有可能嗎 XD)

<img src="{{site.url}}/img/2015-06-21/demo.png" width="45%">
<img src="{{site.url}}/img/2015-06-21/trello.png" width="45%">

<br><br><br>

啊，最後再囉唆一下，說說為什麼會想用 Desktop App 的形式來寫這東西，而不是用已經會的寫網站技術去寫一個網站就好

1. 沒錯，因為手癢想玩 XD，呵呵，因為 Mobile、Web 我都算會一點了，所以要是再略懂 Destop 的話，那不就無敵了嗎 (大誤)

1. 主要還是看上 Electron 的 Cross-platform 特性啦，畢竟公家機關才不會跟你一起使用 MAC 勒

1. 這個 Application 本質上確實是有需要在離線情況下使用的

<br><br>

<img src="{{site.url}}/img/2015-06-21/ya.jpg" width="45%">

## 呼～～～ 科技，始終來自於惰性～～ Ya ( ′-`)y-～

<br>
