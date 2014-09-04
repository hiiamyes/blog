---
layout: post
---

ViewPager 是個很基本的 UI 元件，大家應該或多或少都用過

但今天，我突然想要 Duolingo app 中的這種 paging 效果（可以看到上一頁和下一頁），該怎麼做呢？

<img src="{{site.url}}/img/2014-09-04/duolingo-viewpager.gif">

首先
---

我在網路上 survey 的過程中找到了很不錯的一篇文章，裡面提供了三種方法

[Multiple-View ViewPager Options][survey]

我有實際使用了第一種，修改 Adapter 的 getWidth() 方法，但有點不合需求（第一頁的左邊沒有 offset）

第二種方法我跳過ＸＤ

第三種方法我只有瀏覽瀏覽而已，因為不是很想自己在 ViewPager 外再包一層 custom container

不過
---

第三種方法倒是讓我知道了 ViewGroup 有個 [clipToPadding] 的 attr. 可以使用！

這可是非常關鍵的一個東西呀！！（真是孤陋寡聞ＸＤ）

透過設定 ViewPager 的 padding value

再把它的 clipToPadding 改設成 true（ViewPager 本身就繼承自 ViewGroup） 

我們就能夠～～

1. 不需要透過 Adapter 裡的 getWidth 方法也能讓 Page 變小（因為設定了 padding 的關係！）
1. 因為設定了 clipToPadding = true，所以可以看到***原本隱藏在 padding 裡的***上一頁與下一頁

結果！
---

<img src="{{site.url}}/img/2014-09-04/multi-view-viewpager.gif">

{% highlight xml %}
fragment_main.xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <android.support.v4.view.ViewPager
        android:id="@+id/pager"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="#440000ff"
        android:padding="50dp"
        android:clipToPadding="false" />
</LinearLayout>

fragment_page.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="400dp"
    android:padding="20dp"
    android:background="#77ffff00">
    <TextView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="center"
        android:text="Blue is fragment_main\nwith 50dp padding\n\nYellow is fragment_page\nwith 20dp padding\n\nGreen is TextView"
        android:textSize="24sp"
        android:background="#00ff00" />
</LinearLayout>
{% endhighlight %}

[Source Code on Github][source]


後記
---

當然，像 Duolingo 那樣的縮放效果我還不會做ＸＤ

留待下次囉～！


[survey]: http://commonsware.com/blog/2012/08/20/multiple-view-viewpager-options.html
[clipToPadding]: http://developer.android.com/reference/android/view/ViewGroup.html#attr_android:clipToPadding
[source]: https://github.com/hiiamyes/smallCode/tree/master/android/MultiViewViewPager
