---
title: 前端性能优化常用方法
categories: web
tags: [性能优化, CSS]
---

JS中，事件是指用户或浏览器自身执行的某种动作。如click(点击事件)、mouse***(鼠标事件)。事件流是指页面中接收事件的顺序,也可理解为事件在页面中传播的顺序。


<!-- more -->

## 网页内容

**1.1 减少http请求次数**

**1.1.1**  **捆绑文件**

通过一些现成的库将多个脚本文件捆绑成一个文件，将多个样式表文件捆绑成一个文件，以此来减少文件的下载次数。

**1.1.2**  **CSS Sprites**

把多个图片拼成一副图片，然后通过CSS来控制需要显示图片的位置（ [CSS Sprites Generator](https://www.toptal.com/developers/css/sprite-generator)）

**1.1.3**  **Inline images**

通过Base64编码的字符串将图片内嵌到网页文本中。（但是只适合用于小图标，大一点的图片就免了）

**1.2 减少DNS查询次数**

DNS（Domain Name System，域名系统）

**1.3**  **避免页面跳转**

**1.4**  **缓存Ajax**

**1.5**  **延迟加载**

这里讨论延迟加载需要我们知道我们的网页最初加载需要的最小内容集是什么。剩下的内容就可以推到延迟加载的集合中。

Javascript是典型的可以延迟加载内容。一个比较激进的做法是开发网页时先确保网页在没有Javascript的时候也可以基本工作，然后通过延迟加载脚本来完成一些高级的功能。

**1.6**  **提前加载**

与延迟加载目的相反，提前加载的是为了提前加载接下来网页中访问的资源，下面是提前加载的类型

无条件提前加载：当前网页加载完成后，马上去下载一些其他的内容。例如google会在页面加载成功之后马上去下载一个所有结果中会用到的image sprite。

**1.7**  **减少DOM元素数量**

网页中元素过多对网页的加载和脚本的执行都是沉重的负担，500个元素和5000个元素在加载速度上会有很大差别。

想知道你的网页中有多少元素，通过在浏览器中的一条简单命令就可以算出，

document.getElementsByTagName(&#39;\*&#39;).length

参考： [https://www.cnblogs.com/chenxizhang/archive/2013/05/17/3083162.html](https://www.cnblogs.com/chenxizhang/archive/2013/05/17/3083162.html)

[http://www.cnblogs.com/huyh/archive/2009/03/30/1422976.html](http://www.cnblogs.com/huyh/archive/2009/03/30/1422976.html)

- 避免不正确地使用服务器控件。
- 减少不必要的内容（并不是所有内容都必须放在页面上面的）

        如果数据量大，可以考虑分页，或者按需加载

**1.8**  **根据域名划分内容**

浏览器一般对同一个域的下载连接数有所限制，按照域名划分下载内容可以浏览器增大并行下载连接，但是注意控制域名使用在2-4个之间，不然dns查询也是个问题。

**1.9**  **减少iframe数量**

使用iframe要注意理解iframe的优缺点

优点

- 可以用来加载速度较慢的内容，例如广告。
- [安全沙箱保护](http://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/)。浏览器会对iframe中的内容进行安全控制。
- 脚本可以并行下载

缺点

- 即使iframe内容为空也消耗加载时间
- 会阻止页面加载
- [没有语义](http://www.w3schools.com/html/html5_semantic_elements.asp)

**1.10**  **避免404**

404我们都不陌生，代表服务器没有找到资源，我们要特别要注意404的情况不要在我们提供的网页资源上，客户端发送一个请求但是服务器却返回一个无用的结果，时间浪费掉了。

更糟糕的是我们网页中需要加载一个外部脚本，结果返回一个404，不仅阻塞了其他脚本下载，下载回来的内容(404)客户端还会将其当成Javascript去解析。

## **服务器**

**2.1**  **使用CDN**

再次强调第一条黄金定律，减少网页内容的下载时间。提高下载速度还可以通过CDN(内容分发网络)来提升。CDN通过部署在不同地区的服务器来提高客户的下载速度。

**2.2**  **添加Expires 或Cache-Control报文头**

**2.3**  **Gzip压缩传输文件**

**2.4**  **配置ETags**

**2.5**  **尽早flush输出**

**2.6**  **使用GET Ajax请求**

浏览器在实现XMLHttpRequest POST的时候分成两步，先发header，然后发送数据。而GET却可以用一个TCP报文完成请求。另外GET从语义上来讲是去服务器取数据，而POST则是向服务器发送数据，所以我们使用Ajax请求数据的时候尽量通过GET来完成。

**2.7**  **避免空的图片src**

空的图片src仍然会使浏览器发送请求到服务器，这样完全是浪费时间，而且浪费服务器的资源。尤其是你的网站每天被很多人访问的时候，这种空请求造成的伤害不容忽略。

 所以注意我们的网页中是否存在这样的代码：

straight HTML
                &lt;img src=&quot;&quot;&gt;

JavaScript
                var img = new Image();
                img.src = &quot;&quot;;

## **Cookie**

**3.1**  **减少Cookie大小**

**3.2**  **页面内容使用无cookie域名**

## **CSS**

**4.1**  **将样式表置顶**

将样式表(css)放在网页的HEAD中会让网页显得加载速度更快，因为这样做可以使浏览器逐步加载已将下载的网页内容。这对内容比较多的网页尤其重要，用户不用一直等待在一个白屏上，而是可以先看已经下载的内容。

如果将样式表放在底部，浏览器会拒绝渲染已经下载的网页，因为大多数浏览器在实现时都努力避免重绘，样式表中的内容是绘制网页的关键信息，没有下载下来之前只好对不起观众了。

**4.2**  **避免CSS表达式**

CSS表达式可以动态的设置CSS属性，在IE5-IE8中支持，其他浏览器中表达式会被忽略。例如下面表达式在不同时间设置不同的背景颜色。

CSS表达式的问题在于它被重新计算的次数远比我们想象的要多，不仅在网页绘制或大小改变时计算，即使我们滚动屏幕或者移动鼠标的时候也在计算，因此我们还是尽量避免使用它来防止使用不当而造成的性能损耗。

如果想达到类似的效果我们可以通过简单的脚本做到。

**4.3**  **用&lt;link&gt;代替@import**

避免使用@import的原因很简单，因为它相当于将css放在网页内容底部。

**4.4**  **避免使用Filters**

[AlphaImageLoad](http://msdn.microsoft.com/en-us/library/ms532969(v=vs.85).aspx)也是IE5.5 - IE8中支持，这种滤镜的使用会导致图片在下载的时候阻塞网页绘制，另外使用这种滤镜会导致内存使用量的问题。IE9中已经不再支持。

## **Javascript**

**5.1**  **将脚本置底**

因此对于脚本提速，我们可以考虑以下方式，

- 把脚本置底，这样可以让网页渲染所需要的内容尽快加载显示给用户。
- 现在主流浏览器都支持 [defer](http://www.w3schools.com/tags/att_script_defer.asp)关键字，可以指定脚本在文档加载后执行。
- HTML5中新加了 [async](http://www.w3schools.com/tags/att_script_async.asp)关键字，可以让脚本异步执行。

**5.2**  **使用外部Javascirpt和CSS文件**

使用外部Javascript和CSS文件可以使这些文件被浏览器缓存，从而在不同的请求内容之间重用。

同时将Javascript和CSS从inline变为external也减小了网页内容的大小。

使用外部Javascript和CSS文件的决定因素在于这些外部文件的重用率，如果用户在浏览我们的页面时会访问多次相同页面或者可以重用脚本的不同页面，那么外部文件形式可以为你带来很大的好处。但对于用户通常只会访问一次的页面，例如microsoft.com首页，那inline的javascript和css相对来说可以提供更高的效率。

**5.3**  **精简Javascript和CSS**

        精简就是将Javascript或CSS中的空格和注释全去掉，精简的工具很多，主要可以参考如下，

JS compressors:

- [Packer](http://dean.edwards.name/packer/)
- [JSMin](http://crockford.com/javascript/jsmin)
- [Closure compiler](http://code.google.com/intl/pl/closure/compiler/)
- [YUICompressor](http://developer.yahoo.com/yui/compressor/) (also does CSS)
- [AjaxMin](http://ajaxmin.codeplex.com/) (also does CSS)

CSS compressors:

- [CSSTidy](http://csstidy.sourceforge.net/)
- [Minify](http://code.google.com/p/minify/)
- [YUICompressor](http://developer.yahoo.com/yui/compressor/) (also does JS)
- [AjaxMin](http://ajaxmin.codeplex.com/) (also does JS)
- [CSSCompressor](http://www.csscompressor.com/)

与VS集成比较好的工具如下.

- [YUICompressor](http://yuicompressor.codeplex.com/) - 编译集成，包含在 [NuGet](http://nuget.org/List/Packages/YUICompressor.NET).
- [AjaxMin](http://ajaxmin.codeplex.com/)  - 编译集成

**5.4** [**去除重复脚本**](http://developer.yahoo.com/performance/rules.html#js_dupes)

**5.5**  **减少DOM访问**

通过Javascript访问DOM元素没有我们想象中快，元素多的网页尤其慢，对于Javascript对DOM的访问我们要注意

- 缓存已经访问过的元素
- Offline更新节点然后再加回DOM Tree
- 避免通过Javascript修复layout

**5.6**  **使用智能事件处理**

这里说智能的事件处理需要开发者对事件处理有更深入的了解，通过不同的方式尽量少去触发事件，如果必要就尽早的去处理事件。

比如一个div中10个按钮都需要事件句柄，那么我们可以将事件放在div上，在事件冒泡过程中捕获该事件然后判断事件来源。

## **图片**

**6.1**  **优化图像**

**6.2**  **优化CSS Sprite**

**6.3**  **不要在HTML中缩放图片**

不要通过图片缩放来适应页面，如果你需要小图片，就直接使用小图片吧。

**6.4**  **使用小且可缓存的favicon.ico**

网站图标文件favicon.ico，不管你服务器有还是没有，浏览器都会去尝试请求这个图标。所以我们要确保这个图标

- 存在
- 文件尽量小，最好小于1k
- 设置一个长的过期时间

## **移动客户端**

**7.1**  **保持单个内容小于25KB**

这限制是因为iphone，他只能缓存小于25K，注意 **这是解压后的大小** 。所以单纯gzip不一定够用，精简文件工具要用上了。

**7.2**  **打包组建成符合文档**

把页面内容打包成复合文本就如同带有多附件的Email，它能够使你在一个HTTP请求中取得多个组建。当你使用这条规则时，首先要确定用户代理是否支持（iPhone不支持）。
