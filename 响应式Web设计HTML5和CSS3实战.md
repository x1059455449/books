# 响应式Web设计HTML5和CSS3实战

**申明：本文所使用的例子和部分引文均来源于《响应式Web设计HTML5和CSS3实战（第二版》，如有侵权请联系本人，立即删除，再来就是希望各位支持正版书籍。**

**本文例子的效果一个一个粘贴上去看效果，配合阮一峰的Flex教程，一天可以基本熟悉Flex布局**

## 现在开始

> max-width: 100% 和 width: 100%;

    max-width规则，就是要保证所有图片最大显示为其自身的100%（即最大只可以显示为自身那么大）。此时，如果包含图片的元素（比如包含图片的body或div）比图片固有宽度小，图片会缩放占满最大可用空间

    要实现图片的自动缩放，也可以使用更通用的 width 属性，比如width:100%。如果给width属性设置一个值，那么图片就会按照该值显示，不考虑自身固有宽度。以LOGO（同样也是一张图片）为例，这条规则会导致它显示得跟它的容器一样宽。在容器比图片宽得多的情况下，图片会被无谓地拉伸。

> rem 

    基本上所有浏览器默认的文本大小都是16像素，因此用像素值除以16就可以得到rem值

### 推荐阅读

[http://benfrain.com/just-use-pixels](http://benfrain.com/just-use-pixels)

[https://alistapart.com/articles/](https://alistapart.com/articles/)

[https://patrickhlauke.github.io/getting-touchy-presentation/](https://patrickhlauke.github.io/getting-touchy-presentation/)

    Sass 和 Compass设计师指南

[阮一峰教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

### 布局练习

[https://www.sunforson.com/](https://www.sunforson.com/)

    京东淘宝等各大主页

### 阻塞渲染的CSS（摘自P24）

    从浏览器的角度看，CSS属于“阻塞渲染”的资源。换句话说，浏览器需要下载并解析链接的CSS文件，然后再渲染页面。

    不过，现代浏览器都很聪明，知道哪些样式表（在头部通过媒体查询链接的样式表）必须立即分析，而哪些样式可以等到页面初始渲染结束后再处理。

    在这些浏览器看来，不符合媒体查询指定条件（比如屏幕比媒体查询指定的小）的CSS文件可以延缓执行（deferred），到页面初始加载后再处理，以便让用户感觉页面加载速度更快。

    关于这方面内容，可以参考谷歌开发者网站的文章“阻塞渲染的CSS”①：https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css（短链接：http://t.cn/Rqn0XEt）。
    我想重点向大家介绍这一段：

    “请注意，「阻塞渲染」仅是指该资源是否会暂停浏览器的首次页面渲染。无论CSS是否阻塞渲染，CSS资源都会被下载，只是说非阻塞性资源的优先级比较低而已。”

    再强调一次，所有链接的文件都会被下载下来，只是如果有的文件不必立即应用，那浏览器就不会让它影响页面的渲染。

    因此，如果浏览器要加载的响应式页面（参见example_02-03）通过不同的媒体查询链接了4个不同的样式表（分别为不同视口的设备应用样式），那它就会下载4个CSS文件，但在渲染页面之前，它只会解析那个针对当前视口大小的样式表。

### Flex弹性布局

> 垂直居中文本

```
<div class="CenterMe">
    Hello, I'm centered with Flexbox!
</div>

```
```
.CenterMe {
    background-color: indigo;
    color: #ebebeb;
    font-family: 'Oswald', sans-serif;
    font-size: 2rem;
    text-transform: uppercase;
    height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
} 

```
>> 核心代码

```
    .CenterMe {
    /* 其他属性 */
    display: flex;
    align-items: center;
    justify-content: center;
    } 

```
+ display: flex：这是Flexbox的根本所在。这里就是把当前元素设置为一个Flexbox（而
不是block或inline-block之类的）。

+ align-items：这是要在Flexbox中沿交叉轴对齐项目（在这个例子中垂直居中文本）。

+ justify-content：在这里设置内容沿主轴居中。在Flexbox中，可以把它想象成Word
软件中的一个按钮，用于左、中、右对齐文本

> 偏移

```
<div class="MenuWrap">
    <a href="#" class="ListItem">Home</a>
    <a href="#" class="ListItem">About Us</a>
    <a href="#" class="ListItem">Products</a>
    <a href="#" class="ListItem">Policy</a>
    <a href="#" class="LastItem">Contact Us</a>
</div> 

```
```
.MenuWrap {
    background-color: indigo;
    font-family: 'Oswald', sans-serif;
    font-size: 1rem;
    min-height: 2.75rem;
    display: flex;
    align-items: center;
    padding: 0 1rem; 
}
.ListItem,
.LastItem {
    color: #ebebeb;
    text-decoration: none;
}
.ListItem {
    margin-right: 1rem;
}
.LastItem {
    margin-left: auto;
} 

```

> 反序 

    给包含元素的CSS加一行flex-direction: row-reverse，把最后一项的marginleft: auto改成margin-right: auto；

> 垂直和垂直反向

```
.MenuWrap {
    background-color: indigo;
    font-family: 'Oswald', sans-serif;
    font-size: 1rem;
    min-height: 2.75rem;
    display: flex;
    flex-direction: column-reverse;//column
    align-items: center;
    padding: 0 1rem;
}
.ListItem,
.LastItem {
    color: #ebebeb;
    text-decoration: none;
}

```

> 简单的响应式

```
.MenuWrap { 
    background-color: indigo;
    font-family: 'Oswald', sans-serif;
    font-size: 1rem;
    min-height: 2.75rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0 1rem;
}
@media (min-width: 31.25em) {
 .MenuWrap {
    flex-direction: row;
 }
}
.ListItem,
.LastItem {
    color: #ebebeb;
    text-decoration: none;
}
@media (min-width: 31.25em) {
 .ListItem {
    margin-right: 1rem;
 }
 .LastItem {
    margin-left: auto;
 }
}
```

### Flex弹性盒

> 例子

```
<div class="FlexWrapper">
    <div class="FlexInner">I am content in the inner Flexbox.</div>
</div>
```
``` 
.FlexWrapper {
    background-color: indigo;
    display: flex;
    height: 200px;
    width: 400px;
}
.FlexInner {
    background-color: #34005B;
    display: flex;
    height: 100px;
    width: 200px;
} 

```
+ align-items

```
.FlexWrapper {
    background-color: indigo;
    display: flex;
    height: 200px;
    width: 400px;
    align-items: center;
}
```

+ align-self

```
<div class="FlexWrapper">
    <div class="FlexInner">I am content in the inner Flexbox1.</div>
    <div class="AlignSelf">I am content in the inner Flexbox2.</div>
    <div class="FlexInner">I am content in the inner Flexbox3.</div>
</div>
```
```
.FlexWrapper {
    background-color: indigo;
    display: flex;
    height: 200px;
    width: 400px;
}
.FlexInner {
    background-color: #34005B;
    display: flex;
    height: 100px;
    width: 200px;
}
.AlignSelf {
    align-self: flex-end;
}
```
> align-self的值

     flex-start：把元素的对齐设置为flex-start，可以让元素从Flexbox父元素的起始边开始。

     flex-end：把元素的对齐设置为flex-end，会沿Flexbox父元素的末尾对齐该元素。

     center：把元素放在Flexbox元素的中间。

     baseline：让Flexbox元素中的所有项沿基线对齐。

     stretch：让Flexbox中的所有项（没交叉轴）拉伸至与父元素一样大。

+ justify-content

> 值(前三个看阮一峰的效果，主要是后面两个)

     flex-start
     flex-end
     center
     space-between
     space-around

> 例子

```
<div class="FlexWrapper">
    <div class="FlexInner">I am content in the inner Flexbox 1.</div>
    <div class="FlexInner">I am content in the inner Flexbox 2.</div>
    <div class="FlexInner">I am content in the inner Flexbox 3.</div>
</div> 
```
```
.FlexWrapper {
    background-color: indigo; 
    display: flex;
    justify-content: space-between;//space-around改变这两个值看效果
    height: 200px;
    width: 100%;
}
.FlexInner {
    background-color: #34005B;
    display: flex;
    height: 100px;
    width: 25%;
}
```

+ flex:1

![](flex1.png)
```
 flex-grow（传给flex的第一个值）是相对于其他伸缩项，当前伸缩项在空间允许的情况下可以伸展的量。
 flex-shrink是在空间不够的情况下，当前伸缩项相对于其他伸缩项可以收缩的量。
 flex-basis（传给flex的最后一个值）是伸缩项伸缩的基准值。
```

**几个拓展**

- flex: 1 2 auto:在有空间的情况下可以伸展1部分，在空间不足时可以收缩1部分，而基准大小是内容的固有宽度（即不伸缩的情况下内容的大小）

- flex: 0 0 50px:这个伸缩项既不伸也不缩，基准为50像素（即无论是否存在自由空间，都是50像素）

- flex: 2 0 50%:会多占用两个可用空间，不收缩，基准为50%

- 将flex-shrink的值设置为0，flex-basis实际上就相当于最小宽度

> 例子
```
<div class="FlexWrapper">
    <div class="FlexItems FlexOne">I am content in the inner Flexbox</div>
    <div class="FlexItems FlexTwo">I am content in the inner Flexbox</div>
    <div class="FlexItems FlexThree">I am content in the inner Flexbox</div>
</div>
```
```
.FlexItems {
    border: 1px solid #ebebeb;
    background-color: #34005B;
    display: flex;
    height: 100px;
}
.FlexOne {
    flex: 1.5 0 auto;
}
.FlexTwo,
.FlexThree {
    flex: 1 0 auto;
}
```
在这个例子中，FlexOne占用的空间是FlexTwo和FlexThree所占用空间的1.5倍

## 固定页脚

```
<div class="MainContent">
    Here is a bunch of text up at the top. But there isn't enough
    content to push the footer to the bottom of the page.
</div>
<div class="Footer">
    However, thanks to flexbox, I've been put in my place.
</div> 
```
```
html,
body {
    margin: 0;
    padding: 0;
}
html {
    height: 100%;
}
body {
    font-family: 'Oswald', sans-serif;
    color: #ebebeb;
    display: flex;
    flex-direction: column;
    min-height: 100%;
}
.MainContent {
    flex: 1;
    color: #333;
    padding: .5rem;
    border:1px solid ;
}
.Footer {
    background-color: violet;
    padding: .5rem;
}
```
## order

```
<div class="FlexWrapper">
 <div class="FlexItems FlexHeader">I am content in the Header.</div>
 <div class="FlexItems FlexSideOne">I am content in the SideOne.</div>
 <div class="FlexItems FlexContent">I am content in the Content.</div>
 <div class="FlexItems FlexSideTwo">I am content in the SideTwo.</div>
 <div class="FlexItems FlexFooter">I am content in the Footer.</div>
</div> 
```
```
.FlexWrapper {
    background-color: indigo;
    display: flex;
    flex-direction: column;
}
.FlexItems {
    display: flex;
    align-items: center;
    min-height: 6.25rem; 
    padding: 1rem;
}
.FlexHeader {
    background-color: #105B63;
}
.FlexContent {
    background-color: #FFFAD5;
}
.FlexSideOne {
    background-color: #FFD34E;
}
.FlexSideTwo {
    background-color: #DB9E36;
}
.FlexFooter {
    background-color: #BD4932;
}
```
```
<!-- 加一句 -->
.FlexContent {
    background-color: #FFFAD5;
    order: -1;
} 
```
```
<!-- 常规网页布局 -->
@media (min-width: 30rem) {
.FlexWrapper { 
    flex-flow: row wrap;
}
.FlexHeader {
    width: 100%;
}
.FlexContent {
    flex: 1;
    order: 3;
}
.FlexSideOne {
    width: 150px;
    order: 2;
}
.FlexSideTwo {
    width: 150px;
    order: 4;
}
.FlexFooter {
    width: 100%;
}
} 
```
## 响应式图片

> 实现响应式图片的最简单语法

```
<img src="scones_small.jpg" srcset="scones_medium.jpg 1.5x, scones_large.jpg 2x" alt="Scones taste amazing"> 
```

> srcset 及 sizes 联合切换

```
<img srcset="scones-small.jpg 450w, scones-medium.jpg 900w" sizes="(min-width: 17em) 100vw, (min-width: 40em) 50vw" src="sconessmall.jpg" alt="Scones">
```
这里照样使用了srcset属性。不过，这一次在指定图片描述时，我们添加了以w为后缀的值。这个值的意思是告诉浏览器图片有多宽。这里表示图片分别是450像素宽（scones-small.jpg）和900像素宽（scones-medium.jpg）。但这里以w为后缀的值并不是“真实”大小，它只是对浏览器的一个提示，大致等于图片的“CSS像素”大小。

> picture 元素(不同的视口提供不同的图片)

```
<picture>
 <source media="(min-width: 30em)" srcset="cake-table.jpg">
 <source media="(min-width: 60em)" srcset="cake-shop.jpg">
 <img src="scones.jpg" alt="One way or another, you WILL getcake.">
</picture> 
```
## 响应式视频(离线优先)

http://embedresponsively.com/

http://alistapart.com/articles/

因此我赞成虽然可以使用离线Web应用（有一个不错的教程：http://diveintohtml5.info/offline.html）和LocalStorage（或它们的组合）实现离线优先的体验，但其实我们刚刚有了一个不
错的方案，那就是Service Workers（https://www.w3.org/TR/service-workers/）。

## HTML5新标签（我觉得）

    <detail>和<summary>元素 
    <figure>和<figcaption>元素 
    <article>元素 
    <nav>元素 
    <address>元素
    <video></video>（或<audio></audio>）

## CSS 技巧

+ CSS 响应式多列布局

使用CSS多列布局可以通过几种方式让文本分成多列显示。可以给每一列设定固定的列宽（比如12em），也可以指定内容需要填充的列（比如3）。下面就用代码说明以上做法。要设定列宽，使用以下语法：
```
main {
 column-width: 12em;
}
```
以上代码的意思就是内容要填充的列宽度为12em，无论视口多宽。改变视口宽度会动态改变列数。具体可以看一下example_05-01（或者访问GitHub仓库：https://github.com/benfrain/rwd）。

1. 固定列数，可变宽度
如果想让列数固定，宽度可变，可以这样写规则：
```
main {
 column-count: 4;
}
```
2. 添加列间距和分隔线
还可以给列间添加间距和分隔线：
```
main {
 column-gap: 2em;
 column-rule: thin dotted #999;
 column-width: 12em;
} 
```
+ 断字

    word-wrap: break-word; 例如URL自动换行

+ 省略号
```
    .truncate {
    width: 520px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: no-wrap;
    } 
```

+ 水平滚动面板

```
.Scroll_Wrapper {
 width: 100%;
 white-space: nowrap;
 overflow-x: auto;
 overflow-y: hidden;
}
.Item {
 display: inline-flex;
} 
```

> ::before和::after伪元素

如果查询示例代码，你会发现::before伪元素用于显示项目的数量。如果使用伪元素，记住为了保证::before和::after显示，它们必须包含一个content值，就算空白也行。显示之后，这些元素就好像相应元素的第一个和最后一个子元素一样。

+ 兼容

```
.Scroll_Wrapper {
 width: 100%;
 white-space: nowrap;
 overflow-x: auto;
 overflow-y: hidden;
 /* 在WebKiet的触摸设备上出现 */
 -webkit-overflow-scrolling: touch;
 /* 在支持的IE中删除滚动条 */
 -ms-overflow-style: none;
}
/* 防止WebKit浏览器中出现滚动条 */
.Scroll_Wrapper::-webkit-scrollbar {
 display: none;
} 
```
## 第五章 CSS3新特性（新 CSS3 选择符）


## 第六章

> CSS生成器

http://www.colorzilla.com/gradient-editor/


可视化这些曲线通常更简单，所以我向你推荐http://cubic-bezier.com/和http://easings.net/

正则：http://www.regexr.com/
CSS（很好用的工具）：https://www.webpagetest.org/