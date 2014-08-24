 
先後試用了 Logdown 和 Blogger 後覺得，決定再換來 GitHub Pages 試試，而

1. Logdown 雖然環境不錯，但還沒付費的我 30 張圖片的上傳上限已經爆了
1. Blogger 就像過去的寫作環境一樣，雖然不支援 markdown，但能改文字顏色這點我還是滿喜歡的，不過最後，還是因為貼 gist 很麻煩，以及圖片會自動跑進 google+ 這兩點，讓我果斷的放棄使用

---

Github Pages 的架構我自己把它區分為三部分

1. git repository			: [usernmae].github.io
1. static site generator 	: [jekyll][]
1. templating language		: [liquid][]

簡單來說，就是整個網站放在 github 上，然後透過 jekyll 把檔案轉成 html、css 變成網頁，而其中轉成 markdown 轉成 html 的部分，會使用 [liquid][] 這套 templating language。

按照 [github pages][] 中的 tutorial，很快的就能把 repository 和 jekyll 的環境建立起來，大致上的步驟為：

1. create a git repository on Github with the name [username].github.io
1. installing [jekyll][]

	gem install bundler
	create a Gemfile
		source 'https://rubygems.org'
		gem 'github-pages'
	bundle install

到這邊都滿順利的，但接下來的部分卻讓我搞了很久...

1. create a index.html
2. create a folder _posts
3. create a 2014_08_24_hello_github_pages

上面這三步驟能夠建立出一個首頁 + 一篇 post，首頁的部分就像在寫一般 html 一樣，例如這樣寫

<script src="https://gist.github.com/hiiamyes/ccd5b41ddde5b7be8b91.js"></script>

就能在 gp. 上看到



而在首頁中，為了能建立出 index of post 

所以我們在 <body> 中加入這一段

	<ul>
        {% for post in site.posts %}
        <li>
            <a href="{{ post.url }}">{{ post.title }}</a>
        </li>
        {% endfor %}
    </ul>

不過如果就這樣 deploy 的話，會變成這樣



我就是在這邊被困擾了很久不知道哪裡出錯哈哈，後來才突然想到，這情形和 Angularjs 沒有正常 work 的情況很像，所以推測，應該是 Liquid 沒有正常發揮作用造成的，而要讓


[github pages]: https://pages.github.com/ "Github Pages"
[jekyll]: http://jekyllrb.com/ "Jekyll"
[liquid]: http://docs.shopify.com/themes/liquid-documentation/basics "Liquid"
[creating pages]: https://help.github.com/articles/creating-pages-with-the-automatic-generator "Creating Pages"




