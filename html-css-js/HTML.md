# HTML
html is hypertext markup language由欧洲核子研究中心的物理学家蒂姆·伯纳斯-李（Tim Berners-Lee）发明。
它的最大特点是支持超链接，点击链接就可以跳转到其他网页，从而构成整个互联网。  
浏览器的网页开发设计三种技术，HTML，CSS和Javascript。  
- HTML定义网站的结构和内容  
- CSS样式表定义网页的样式  
- Javascript定义网页和用户的互动行为  

## 1. 网页的基本概念
### 1.1 标签  
网页的 HTML 代码由许许多多不同的标签（tag）构成。学习 HTML 语言，就是学习各种标签的用法。  
HTML 语言忽略缩进和换行

note:https://www.w3cplus.com/a11y/writing-html-with-accessibility-in-mind.html
这篇文章对html标签及语义化讲解的非常好，值得一读。

### 1.2 元素  
浏览器渲染网页时，会把 HTML 源码解析成一个标签树，每个标签都是树的一个节点（node）。这种节点就称为网页元素（element）。
所以，“标签”和“元素”基本上是同义词，只是使用的场合不一样：标签是从源码角度来看，元素是从编程角度来看，比如p标签对应网页的p元素。  
==嵌套的标签就构成了网页元素的层级关系。==
### 1.3 块级元素，行内元素
### 1.4 属性  
属性不区分大小写，用来定制标签的行为  
## 2. 网页的基本标签  
```
<!DOCTYPE>  
<!DOCTYPE html>
<html>  
<html lang="zh-CN">

<head>  
    <meta>
    <link>
    <title>
    <style>
    <script>
    <noscript>
    <base>  
<meta>  
<meta charset="utf-8">  
<meta name="viewport" content="width=device-width, initial-scale=1">  
```
meta表示元数据，用于设置或者说明网页的元数据，网页可以有多个meta标签，meta标签约定放在head内容的最前面。常见的元数据有keywords, description, author, etc。  
```
<title>  
<body>  
```
## 3. 空格和换行  
HTML忽略内容的头部和尾部的空格，会合并内容中间的空格成制表符\t，html还会将文本里面的换行\n和回车\r，替换成空格。  
## 4. 注释  
```
<!-- words -->  
```
注释内容不会显示在网页上，但可以在源代码中查看。  

## 5. URL简介  
url是“统一资源定位符”uniform resource locator"的首字母缩写，中文是网址  
### url的组成部分  
#### 协议scheme  
协议是浏览器请求服务器资源的方法，互联网支持多种协议，必须指明网址使用哪一种协议，默认http协议。其他还有邮件协议**mailto:**后面只有一个冒号  
#### 主机host  
主机就是资源所在的网站名或服务器的名字，又称为域名，比如www.sample.com，有些主机只有ip地址，一般出现在局域网  
#### 端口  
同一个域名下可能包含多个网站，他们之间通过端口区分。端口就是一个整数，简单理解就是访问者告诉服务器，想要访问哪个网站。默认端口80，如果省略了这个参数服务器就返回80端口的网站。  
#### 路径path  
路径就是资源在网站上的位置，比如/path/index.html。路径可能只包含目录，不包含文件名，比如/foo/，甚至结尾的斜杠都可以省略。这时，服务器通常会默认跳转到该目录里面的index.html文件（即等同于请求/foo/index.html）
但也可能有其他的处理（比如列出目录里面的所有文件），这取决于服务器的设置。一般来说，访问www.example.com这个网址，很可能返回的是网页文件www.example.com/index.html。  
#### 查询参数  
查询参数（parameter）是提供给服务器的额外信息。参数的位置是在路径后面，两者之间使用?分隔上例是?key1=value1&key2=value2。  
查询参数可以有一组或多组。每组参数都是键值对（key-value pair）的形式，同时具有键名(key)和键值(value)，它们之间使用等号（=）连接。比如，key1=value就是一个键值对，key1是键名，value1是键值。  
多组参数之间使用&连接，比如key1=value1&key2=value2。  
#### 锚点anchor  
锚点（anchor）是网页内部的定位点，使用#加上锚点名称，放在网址的最后，比如#anchor。浏览器加载页面以后，会自动滚动到锚点所在的位置。  
### url字符
url各个部分只能使用以下字符：  
- 26个英语字母（包括大写和小写）  
- 10个阿拉伯数字  
- 连词号（-）  
- 句点（.）  
- 下划线（_）  
### base标签  
base标签指定网页内部的所有相对 URL 的计算基准。整张网页只能有一个base标签，而且只能放在head里面。它是单独使用的标签，没有闭合标签，下面是一个例子。  
```
<head>  
<base href="https://www.example.com/files/" target="_blank">  
</head>  
```
注意，base标签必须至少具有href属性或target属性之一。一旦设置了base，就对整个网页都有效。如果要改变某个链接的行为，只能用绝对链接替代相对链接。
尤其需要注意锚点，这时锚点也是针对base计算的，而不是针对当前网页的 URL。  
## 6. 网页元素的属性  
元素的写法是HTML标签内部的键值对，属性名跟标签名一样，不区分大小写  
### 有些属性是布尔值  
布尔值的属性只有打开和关闭选项，而且此时的属性值可以省略，只要添加了属性就表示打开该属性  
### 全局属性  
全局属性是所有元素都可以使用的属性，也就是可以把下面的属性放在任意一个网页元素上，不过有些属性对某些元素可能不产生意义  
- 6.1 id  
- 6.2 class  
- 6.3 title  
title属性用来为元素添加附加说明  
- 6.4 tabindex  
网页通常使用鼠标操作，但是某些情况下，用户可能希望使用键盘，或者只有键盘可以用。因此，浏览器允许使用 Tab 键，遍历网页元素。
也就是说，只要不停按下 Tab 键，网页的焦点就会从一个元素转移到另一个元素，选定焦点元素以后，就可以进行下一步操作，比如按下回车键访问某个链接，
或者直接在某个输入框输入文字。  
这里就有一个问题，按下 Tab 键的时候，浏览器怎么知道跳到哪一个元素。HTML 提供了tabindex属性，解决这个问题。它的名字的含义，就是 Tab 的顺序（index）。  
    - 负整数：该元素可以获得焦点（比如使用 JavaScript 的focus()方法），但不参与 Tab 键对网页元素的遍历。这个值通常是-1。  
    - 0：该元素参与 Tab 键的遍历，顺序由浏览器指定，通常是按照其在网页里面出现的位置。  
    - 正整数：网页元素按照从小到大的顺序（1、2、3、……），参与 Tab 键的遍历。如果多个元素的tabindex属性相同，则按照在网页源码里面出现的顺序遍历。  
一般来说，tabindex属性最好都设成0，按照自然顺序进行遍历，这样比较符合用户的预期，除非网页有特殊布局。如果网页所有元素都没有设置tabindex，
那么只有那些默认可以遍历的元素（比如链接、输入框等）才能参与 Tab 键的遍历，顺序由其在源码的位置决定。
因此实际上，只有那些无法获得焦点的元素（比如span、div）需要参与遍历，才有必要设置tabindex属性。  
- 6.5 accesskey  
accesskey属性指定网页元素获得焦点的快捷键，该属性的值必须是单个的可打印字符。只要按下快捷键，该元素就会得到焦点。  
accesskey属性的字符键，必须配合功能键，一起按下才会生效。也就是说，快捷键是“功能键 + 字符键”的组合。不同的浏览器与不同的操作系统，功能键都不一样。
比如，Chrome 浏览器在 Windows 系统和 Linux 系统的快捷键是Alt + 字符键，在 Mac 系统的快捷键是Ctrl + Alt + 字符键。
注意，accesskey如果跟操作系统或浏览器级别的快捷键有冲突，这时不会生效。  
- 6.6 style  
- 6.7 hidden  
表示当前元素不再跟页面相关，因此浏览器不会渲染这个元素  
- 6.8 lang, dir  
lang属性指定网页元素使用的语言，dir表示文字阅读方向，有三个可能值：  
    - ltr：从左到右阅读，比如英语。  
    - rtl：从右到左阅读，阿拉伯语、波斯语、希伯来语都属于这一类。  
    - auto：浏览器根据内容的解析结果，自行决定。  
- 6.9 contenteditable  
- 6.10 spellcheck  
- 6.11 data-  
data-属性用于放置自定义数据。如果没有其他属性或元素合适放置数据，就可以放在data-属性。  
```
<a href="#" class="tooltip" data-tip="this is the tip!">链接</a>  
```
上面代码中，data-tip用于放置链接的提示文字。  
## 7. 字符编码  
一般情况下，服务器在向浏览器发送HTML网页文件时，会通过http头部信息声明网页的编码方式。同时，网页内部也会再用meta标签，再次声明网页的编码  

```
Content-Type: text/html; charset=UTF-8  
<meta charset="UTF-8">  
```
### 7.1 常用字符编码  
```
<：&lt;  
>：&gt;  
"：&quot;  
'：&apos;  
&：&amp;  
©：&copy;  
#：&num;  
§：&sect;  
¥：&yen;  
$：&dollar;  
£：&pound;  
¢：&cent;  
%：&percnt;  
*：$ast;  
@：&commat;  
^：&Hat;  
±：&plusmn;  
空格：&nbsp;  
```
## 8. 语义结构
html标签的名称都带有语义semantic，使用时应该尽量符合标签的语义，不要用错误语义的标签。语义良好的网页，天然具有良好的结构，易读易写，易于维护。  
### 含义  
HTML 标签的一个重要作用，就是声明网页元素的性质，使得用户只看标签，就能了解这个元素的意义，阅读 HTML 源码就能了解网页的大致结构。这被称为 HTML 的语义原则。  
下面就是一个典型的语义结构的网页。  

```
<body>
  <header>页眉</header>
  <main>
    <article>
      <h1>文章标题</h1>
      <p>文章内容</p>
    </article>
  </main>
  <footer>页尾</footer>
</body>
```

只看上面的代码，就可以知道，页面分成页眉（header）、主体（main）、页尾（footer）三个部分。  
编写 HTML 网页，第一步就是写出语义结构的网页骨架。  
### 常用标签  
- header  
- footer  
- main  
- article  
- aside  
- section  
- nav  
- h1 ~ h6  
- hgroup  

## 9. 文本标签
历史上，网页的主要功能是文本展示。所以，HTML 提供了大量的文本处理标签。  
### 9.1 文本布局类标签
#### div标签
#### p标签
#### span标签
### 9.2 换行标签
#### br标签
#### wbr标签
wbr标签跟br很相似，表示一个可选的断行。如果一行的宽度足够，则不断行；如果宽度不够，需要断行，就在wbr的位置的断行。
它是为了防止浏览器在一个很长的单词中间，不正确地断行或者不断行，所以事先标明可以断行的位置，主要用于欧洲一些单词很长的语言或者 URL 的断行。  

#### hr标签
该标签是历史遗留下来的，建议尽量避免使用。主题之间的分隔可以使用section，如果想要水平线的效果，可以使用 CSS。  
### 9.3 格式化标签  
#### pre标签  
HTML 标签在pre里面还是起作用的。pre只保留空格和换行，不会保留 HTML 标签。  
#### strong标签和b标签  
它与strong的区别在于，由于历史原因，它没有语义，是一个纯样式的标签，违反了语义与样式分离的原则，因此不建议使用，应该优先使用strong标签  
#### em标签和i标签  
&lt;i&gt;标签的语义不强，更接近是一个纯样式的标签，建议优先使用&lt;em&gt;标签代替它。  
#### sub, sup, var
&lt;var&gt;标签表示代码或数学公式的变量。  
#### u, s标签  
u标签表示需要注意的内容，浏览器会渲染成下划线，要注意区分链接下划线，可以考虑用css改变它的默认样式。  
s标签会为内容添加删除线  
#### blockquote, cit, q
blockquote是一个块级标签，表示引用他人的话。浏览器会在样式上，与正常文本区别显示。  
```
<blockquote cite="https://quote.example.com">
  <p>天才就是 1% 的天赋和99%的汗水。</p>
</blockquote>
<cite>-- 爱迪生</cite>
```
blockquote标签有一个cite属性，它的值是一个网址，表示引言来源，不会显示在网页上。  
cite标签表示引言出处或者作者，浏览器默认使用斜体显示这部分内容。  
q是一个行内标签，也表示引用。它与blockquote的区别，就是它不会产生换行。另外，跟blockquote一样，q也有cite属性，表示引言的来源网址。  
注意，浏览器默认会斜体显示q的内容，并且会自动添加半角的双引号。所以，引用中文内容时要小心  
#### code
code标签是一个行内元素，表示标签内容是计算机代码，浏览器默认会以等宽字体显示。  
#### kbd, samp
kbd标签是一个行内元素，原意是用户从键盘输入的内容，现在扩展到各种输入，包括语音输入。浏览器默认以等宽字体显示标签内容。kbd可以嵌套，方便指定样式。  
samp标签是一个行内元素，表示计算机程序输出内容的一个例子。浏览器默认以等宽字体显示。  
#### mark
是一个行内标签，表示突出显示的内容。Chrome 浏览器默认会以亮黄色背景，显示该标签的内容。  
#### small  
small是一个行内标签，浏览器会将它包含的内容，以小一号的字号显示，不需要使用 CSS 样式。它通常用于文章附带的版权信息或法律信息。  
### 9.4 特殊内容标签  
#### time, data
time是一个行内标签，为跟时间相关的内容提供机器可读的格式。time的datetime属性，用来指定机器可读的日期，可以有多种格式。
data标签与time类似，也是提供机器可读的内容，但是用于非时间的场合。  
- 有效年份：2011
- 有效月份：2011-11
- 有效日期：2011-11-18
- 无年份的日期：11-18
- 年度的第几周：2011-W47
- 有效时间：14:54、14:54:39、14:54:39.929
- 日期和时间：2011-11-18T14:54:39.929
```
<p>运动会预定<time datetime="2015-06-10">下周三</time>举行。</p>  
<p>音乐会在<time datetime="20:00">晚上八点</time>开始。</p>  
<p>本次马拉松比赛第一名是<data value="39">张三</data></p>。  
```
#### address  
address标签是一个块级元素，表示某人或某个组织的联系方式  
该标签有几个注意点。
（1）如果是文章里提到的地址（比如提到搬家前的地址），而不是联系信息，不要使用address标签。
（2）address的内容不得有非联系信息，比如发布日期。
（3）address不能嵌套，并且内部不能有标题标签（h1~h6），也不能有article、aside、section、nav、header、footer等标签。
（4）通常，address会放在footer里面，下面是一个例子。
#### abbr
#### ins, del
```
<del><p>会议定于5月8日举行。</p></del>
<ins><p>会议定于5月9日举行。</p></ins>
```
浏览器默认为del标签的内容加上删除线，为ins标签的内容加上下划线。这两个标签都有以下属性。  
- cite：该属性的值是一个 URL，表示该网址可以解释本次删改。  
- datetime：表示删改发生的时间。  
#### dfn
#### ruby
- rp
- rb
- rt
- rbc, rtc
```
<ruby style="ruby-position: under;">
  <rbc>
    <rb>汉</rb><rp>(</rp><rt>han</rt><rp>)</rp>
    <rb>字</rb><rp>(</rp><rt>zi</rt><rp>)</rp>
  </rbc>
  <rtc style="ruby-position: over;">
    <rp>(</rp><rt>Chinese</rt><rp>)</rp>
  </rtc>
</ruby>
```
#### bdo, bdi  

## 10. 列表标签
- ol, ul
- li
- dl, dt, dd
dl（description list）  
dt（description term）  
dd（description detail）  
dt和dd都是块级元素，dd默认会在dt下方缩进显示。  
```
<dl>
  <dt>CPU</dt>
  <dd>中央处理器</dd>

  <dt>Memory</dt>
  <dd>内存</dd>

  <dt>Hard Disk</dt>
  <dd>硬盘</dd>
</dl>
```
## 11. 图像标签
### img, figure, figcaption
figure标签可以理解为一个图像区块，将图像和相关信息封装在一起。figcaption是它的可选子元素，表示图像的文本描述，通常用于放置标题，可以出现多个。
除了图像，figure还可以封装引言、代码、诗歌等等。它等于是一个将主体内容与附加信息，封装在一起的语义容器。  
```
<figure>
  <img src="#">
  <figcaption>示例图片</figcaption>
  <figcaption>JavaScript 代码示例</figcaption>
  <p><code>const foo = 'hello';</code></p>
</figure>
```
#### srcset属性和sizes属性  
我们知道，img标签用于插入网页图像，所有情况默认插入的都是同一张图像，手机和电脑端插入同一张图片效果明显不好。所以，引入这两个属性来解决这个问题，称之为“响应式图像”  
```
<img srcset="foo-160.jpg 160w,
             foo-320.jpg 320w,
             foo-640.jpg 640w,
             foo-1280.jpg 1280w"
     sizes="(max-width: 440px) 100vw,
            (max-width: 900px) 33vw,
            254px"
     src="foo-1280.jpg">
```
假定当前设备的屏幕宽度是480px，浏览器从sizes属性查询得到，图片的显示宽度是33vw（即33%），等于160px。srcset属性里面，正好有宽度等于160px的图片，于是加载foo-160.jpg。  
### picture  
picture是一个容器标签，内部使用source和img，指定不同情况下加载的图像。  
```
<picture>
  <source srcset="homepage-person@desktop.png,
                  homepage-person@desktop-2x.png 2x"
          media="(min-width: 990px)">
  <source srcset="homepage-person@tablet.png,
                  homepage-person@tablet-2x.png 2x"
          media="(min-width: 750px)">
  <img srcset="homepage-person@mobile.png,
               homepage-person@mobile-2x.png 2x"
       alt="Shopify Merchant, Corrine Anestopoulos">
</picture>
```
picture内部的source标签，主要使用media属性和srcset属性。media属性给出媒体查询表达式，srcset属性就是img标签的srcset属性，给出加载的图像文件。
sizes属性其实这里也可以用，但由于有了media属性，就没有必要了。  
浏览器按照source标签出现的顺序，依次判断当前设备是否满足media属性的媒体查询表达式，如果满足就加载srcset属性指定的图片文件，并且不再执行后面的source标签和img标签。  
img标签是默认情况下加载的图像，用来满足上面所有source都不匹配的情况，或者不支持picture的老式浏览器。  
## 链接标签  
### a标签
```
<a href="https://www.example.com/">
  <img src="https://www.example.com/foo.jpg">
</a>
```
a标签有如下属性：  
- href
- hreflang
- title
- target
- rel
- referrerpolicy
- ping
- type
- download

```
<p><a href="http://foo.com" target="test">foo</a></p>
<p><a href="http://bar.com" target="test">bar</a></p>
```
上面代码中，两个链接都在名叫test的窗口打开。首先点击链接foo，浏览器发现没有叫做test的窗口，就新建一个窗口，起名为test，在该窗口打开foo.com。
然后，用户又点击链接bar，由于已经存在test窗口，浏览器就在该窗口打开bar.com，取代里面已经打开的foo.com。  
target属性的值也可以是以下四个关键字之一  
- _self：当前窗口打开，这是默认值。
- _blank：新窗口打开。
- _parent：上层窗口打开，这通常用于从父窗口打开的子窗口，或者iframe里面的链接。如果当前窗口没有上层窗口，这个值等同于_self。
- _top：顶层窗口打开。如果当前窗口就是顶层窗口，这个值等同于_self。  
注意，使用target属性的时候，最好跟rel="noreferrer"一起使用，这样可以避免安全风险。  
rel属性说明链接与当前页面的关系。下面是一些常见的rel属性的值。  
- alternate：当前文档的另一种形式，比如翻译。
- author：作者链接。
- bookmark：用作书签的永久地址。
- external：当前文档的外部参考文档。
- help：帮助链接。
- license：许可证链接。
- next：系列文档的下一篇。
- nofollow：告诉搜索引擎忽略该链接，主要用于用户提交的内容，防止有人企图通过添加链接，提高该链接的搜索排名。
- noreferrer：告诉浏览器打开链接时，不要将当前网址作为 HTTP 头信息的Referer字段发送出去，这样可以隐藏点击的来源。
- noopener：告诉浏览器打开链接时，不让链接窗口通过 JavaScript 的window.opener属性引用原始窗口，这样就提高了安全性。
- prev：系列文档的上一篇。
- search：文档的搜索链接。
- tag：文档的标签链接。
### 邮件链接
链接也可以指向一个邮件地址，使用mailto协议。用户点击后，浏览器会打开本机默认的邮件程序，让用户向指定的地址发送邮件  
```
<a href="mailto:contact@example.com">联系我们</a>
<a
  href="mailto:foo@bar.com?cc=test@test.com&subject=The%20subject&body=The%20body"
>发送邮件</a>
<a href="mailto:">告诉朋友</a>
```
除了邮箱，邮件协议还允许指定其他几个邮件要素。  
- subject：主题
- cc：抄送
- bcc：密送
- body：邮件内容
- 使用方法是将这些邮件要素，以查询字符串的方式，附加在邮箱地址后面。这些要素的值需要经过 URL 转义，比如空格转成%20。  
不指定邮箱也是允许的，就像下面这样。这时用户自己在邮件程序里面，填写想要发送的邮箱，通常用于邮件分享网页。  
### 电话链接
```
<a href="tel:13312345678">13312345678</a>
```
上面代码在手机中，点击链接会唤起拨号界面，可以直接拨打指定号码。  
### link标签
link标签主要用于将当前网页与相关的外部资源联系起来，通常放在head元素里面。最常见的用途就是加载 CSS 样式表。
#### rel属性
rel属性表示外部资源与当前文档之间的关系，是link标签的必需属性。它可以但不限于取以下值。  
- alternate：文档的另一种表现形式的链接，比如打印版。
- author：文档作者的链接。
- dns-prefetch：要求浏览器提前执行指定网址的 DNS 查询。
- help：帮助文档的链接。
- icon：加载文档的图标文件。
- license：许可证链接。
- next：系列文档下一篇的链接。
- pingback：接收当前文档 pingback 请求的网址。
- preconnect：要求浏览器提前与给定服务器，建立 HTTP 连接。
- prefetch：要求浏览器提前下载并缓存指定资源，供下一个页面使用。它的优先级较低，浏览器可以不下载。
- preload：要求浏览器提前下载并缓存指定资源，当前页面稍后就会用到。它的优先级较高，浏览器必须立即下载。
- prerender：要求浏览器提前渲染指定链接。这样的话，用户稍后打开该链接，就会立刻显示，感觉非常快。
- prev：表示当前文档是系列文档的一篇，这里给出上一篇文档的链接。
- search：提供当前网页的搜索链接。
- stylesheet：加载一张样式表。
#### media属性
media属性给出外部资源生效的媒介条件。  
```
<link href="print.css" rel="stylesheet" media="print">
<link href="mobile.css" rel="stylesheet" media="screen and (max-width: 600px)">
```
上面代码中，打印时加载print.css，移动设备访问时（设备宽度小于600像素）加载mobile.css。  
### script标签
### noscript标签
## 多媒体标签
### video
video标签是一个块级元素，用于放置视频。如果浏览器支持加载的视频格式，就会显示一个播放器，否则显示video内部的子元素。  
### audio
audio标签是一个块级元素，用于放置音频，用法与video标签基本一致。  
### track
track标签用于指定视频的字幕，格式是 WebVTT （.vtt文件），放置在video标签内部。它是一个单独使用的标签，没有结束标签。  
### source
source标签用于picture、video、audio的内部，用于指定一项外部资源。单标签是单独使用的，没有结束标签。
```
<audio controls>
  <source src="foo.mp3" type="audio/mp3">
  <source src="foo.ogg" type="audio/ogg">
  <p>你的浏览器不支持 HTML5 音频，请直接下载<a href="foo.mp3">音频文件</a>。</p>
</audio>
```
### embed
embed标签用于嵌入外部内容，这个外部内容通常由浏览器插件负责控制。由于浏览器的默认插件都不一致，很可能不是所有浏览器的用户都能访问这部分内容，建议谨慎使用。  
### object, param
object标签作用跟embed相似，也是插入外部资源，由浏览器插件处理。它可以视为embed的替代品，有标准化行为，只限于插入少数几种通用资源，没有历史遗留问题，因此更推荐使用。  
```
<object type="application/pdf"
    data="/media/examples/In-CC0.pdf"
    width="250"
    height="200">
</object>
```
## iframe
iframe标签生成一个指定区域，在该区域中嵌入其他网页。它是一个容器元素，如果浏览器不支持iframe，就会显示内部的子元素。  
```
<iframe src="https://www.example.com"
        width="100%" height="500" frameborder="0"
        allowfullscreen sandbox>
  <p><a href="https://www.example.com">点击打开嵌入页面</a></p>
</iframe>
```
## 表格标签
### table, caption
table是一个块级容器标签，所有表格内容都要放在这个标签里面。caption总是table里面的第一个子元素，表示表格的标题。该元素是可选的。  
### thead, tbody, tfoot
thead、tbody、tfoot都是块级容器元素，且都是table的一级子元素，分别表示表头、表体和表尾。  
这三个元素都是可选的。如果使用了 thead ，那么 tbody 和 tfoot 一定在 thead 的后面。如果使用了 tbody ，那么 tfoot 一定在 tbody 后面。  
大型表格内部可以使用多个 tbody ，表示连续的多个部分。  
### colgroup, col  
colgroup是table的一级子元素，用来包含一组列的定义。col是colgroup的子元素，用来定义表格的一列。  
```
<table>
  <colgroup>
    <col>
    <col>
    <col>
  </colgroup>
</table>
```
col不仅是一个单独使用的标签，没有结束标志，而且还是一个空元素，没有子元素。它的主要作用，除了申明表格结构，还可以为表格附加样式。
col有一个span属性，值为正整数，默认为1。如果大于1，就表示该列的宽度包含连续的多列。  
```
<table>
  <colgroup>
    <col class="c1">
    <col class="c2">
    <col class="c3">
  </colgroup>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>3</td>
  </tr>
</table>
```
```
<table>
  <colgroup>
    <col>
    <col span="2">
    <col>
  </colgroup>
</table>
```
上面代码中，表格的表头定义了3列，实际数据有4列。表头的第2列会连续跨2列。
### tr, th, td
tr标签表示表格的一行（table row）。如果表格有thead、tbody、tfoot，那么tr就放在这些容器元素之中，否则直接放在table的下一级。  
th和td都用来定义表格的单元格。其中，th是标题单元格，td是数据单元格。  
```
<table>
  <tr>
    <th>学号</th><th>姓名</th>
  </tr>
  <tr>
    <td>001</td><td>张三</td>
  </tr>
  <tr>
    <td>002</td><td>李四</td>
  </tr>
</table>
```
#### colspan属性，rowspan属性
单元格会有跨越多行或多列的情况，这要通过colspan属性和rowspan属性设置，前者表示单元格跨越的栏数，后者表示单元格跨越的行数。它们的值都是一个非负整数，默认为1。  
#### headers属性
如果表格很大，单元格很多，源码里面会看不清，哪个单元格对应哪个表头，这时就可以使用headers属性。  
```
<table>
  <tr>
    <th id="no">学号</th><th id="names">姓名</th>
  </tr>
  <tr>
    <td headers="no">001</td><td headers="names">张三</td>
  </tr>
  <tr>
    <td headers="no">002</td><td headers="names">李四</td>
  </tr>
</table>
```
#### scope属性
scope属性只有th标签支持，一般不在td标签使用，表示该th单元格到底是栏的标题，还是列的标题。
## 表单标签
表单（form）是用户输入信息与网页互动的一种形式。大多数情况下，用户提交的信息会发给服务器，比如网站的搜索栏就是表单。  
表单由一种或多种的小部件组成，比如输入框、按钮、单选框或复选框。这些小部件称为控件（controls）。  
### form标签
form标签用来定义一个表单，所有表单内容放到这个容器元素之中。
```
<form action="https://example.com/api" method="post">
  <label for="POST-name">用户名：</label>
  <input id="POST-name" type="text" name="user">
  <input type="submit" value="提交">
</form>
```
上面代码就是一个表单，一共包含三个控件：一个label标签，一个文本输入框，一个提交按钮。
其中，文本输入框的name属性是user，表示将向服务器发送一个键名为user的键值对，键值就是这个控件的value属性，等于用户输入的值。  
#### enctype
form表单的enctype属性，指定了采用 POST 方法提交数据时，浏览器给出的数据的 MIME 类型。该属性可以取以下值。  
- application/x-www-form-urlencoded
- multipart/form-data
### fieldset, legend
fieldset标签是一个块级容器标签，表示控件的集合，用于将一组相关控件组合成一组。  
```
<form>
  <fieldset>
    <legend>学生情况登记</legend>
    <p>年龄：<input type="text" name="age"></p>
    <p>性别：<input type="text" name="gender"></p>
  </fieldset>
</form>
```
legend标签用来设置fieldset控件组的标题，通常是fieldset内部的第一个元素，会嵌入显示在控件组的上边框里面。  
### label
label标签是一个行内元素，提供控件的文字说明，帮助用户理解控件的目的。  
### input
input标签是一个行内元素，用来接收用户的输入。它是一个单独使用的标签，没有结束标志。它有多种类型，取决于type属性的值，默认值是text，表示一个输入框  
### button
button标签会生成一个可以点击的按钮，没有默认行为，通常需要用type属性或脚本指定按钮的功能。button内部不仅放置文字，还可以放置图像，这可以形成图像按钮。
```
<button>点击</button>
<button name="search" type="submit">
  <img src="search.gif">搜索
</button>
```
### select
select标签用于生成一个下拉菜单。
```
<label for="pet-select">宠物：</label>

<select id="pet-select" name="pet-select">
  <option value="">--请选择一项--</option>
  <option value="dog">狗</option>
  <option value="cat">猫</option>
  <option value="others">其他</option>
</select>
```
### option, optgroup
option标签用在select、optgroup、datalist里面，表示一个菜单项，参见select的示例。说通俗点就是对下拉选项进行分类说明，但用户不能选中分类  
### datalist
datalist标签是一个容器标签，用于为指定控件提供一组相关数据，通常用于生成输入提示。它的内部使用option，生成每个菜单项。  
```
<label for="ice-cream-choice">冰淇淋：</label>
<input type="text" list="ice-cream-flavors" id="ice-cream-choice" name="ice-cream-choice">

<datalist id="ice-cream-flavors">
  <option value="巧克力">
  <option value="椰子">
  <option value="薄荷">
  <option value="草莓">
  <option value="香草">
</datalist>
```
### textarea
textarea是一个块级元素，用来生成多行的文本框。
### output
output标签是一个行内元素，用于显示用户操作的结果。
### progress
progress标签是一个行内元素，表示任务的完成进度。浏览器通常会将显示为进度条。
### meter
meter标签是一个行内元素，表示指示器，用来显示已知范围内的一个值，很适合用于任务的当前进度、磁盘已用空间、充电量等带有比例性质的场合。
浏览器通常会将其显示为一个不会滚动的指示条。  
```
<p>烤箱的当前温度是<meter min="200" max="500"
  value="350"> 350 度</meter>。</p>
```
## 其他标签
### dialog
dialog标签表示一个可以关闭的对话框。  
### details, summary
details标签用来折叠内容，浏览器会折叠显示该标签的内容。用户点击这段文本，折叠的文本就会展开，显示详细内容。  
summary标签用来定制折叠内容的标题。
