---
title: 移动端项目开发小结
categories: 移动端
tags: [移动端, rem]
---

最近开发移动端项目，发现，与PC端项目开发遇到的浏览器兼容性问题相比，移动端还有更多的坑的。这里将遇到一些问题，做出总结。

<!-- more -->

##  页面自适应

各种手机型号，尺寸大小不一，有的屏幕320px宽，有的屏幕414px宽。。如果尺寸写固定单位px，那么很多元素会变形，就要用媒体查询@media针对不同的屏幕宽度进行调整，太麻烦。所以，推荐在页面中使用rem作为尺寸单位，引入如下代码即可：

```
(function (doc, win) {
    var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
        callback = function () {
            var clientWidth = docEl.clientWidth;
            clientWidth = clientWidth < 640 ? clientWidth : 640;
            docEl.style.fontSize = clientWidth / 6.4 + 'px';
        };

    if (!doc.addEventListener) return;
    callback(); // 防止页面加载时的抖动
    win.addEventListener(resizeEvt, callback, false);
    doc.addEventListener('DOMContentLoaded', callback, false);
})(document, window);
```
如果在640px像素的屏幕下开发，需要为某字体设置16px大小时，只需要设置为0.16rem即可；
如果在320px像素的屏幕下开发，需要为某字体设置16px大小时，只需要设置为0.32rem即可；



## 优化alert弹窗

移动端有些错误需要提示时，使用默认alert函数的效果很不友好。网上很多比较友好的插件可用，但是为了不使项目太大，这里手动封装了一个：
其中element为存放弹出内容的外围div,test为弹出内容，position为弹出框在页面中的位置。
```
function showToast(element, test, position) {
    element.html('<p class="error-content">' + test + '</p>');
    element.stop(true, true).animate({
        bottom: position,
        opacity: '1'
    }, 400).animate({
        opacity: '1'
    }, 1000).animate({
        bottom: '-2rem'
    }, 0);
}
```

使用方法，只需创建如下元素用力存放提示内容，并且设置其定位样式：
```
<div id="error-alert">
    <p class="error-content"></p>
</div>
```
```
#error-alert {
    position: fixed;
    opacity: 1;
    bottom: -2rem;
    left: 50%;
    right: 0;
    width: 6rem;
    height: 1rem;
    line-height: 1rem;
    margin-left: -3rem;
    background: #fff;
    border-radius: 0.5rem;
    z-index: 999;
}

#error-alert.show-error {
    top: 0;
}

#error-alert .error-content {
    color: #333;
    font-size: 0.4rem;
    line-height: 1rem;
    text-align: center;
}
```

## 华为自带浏览器不支持 es6

真机测试时，发现在华为手机自带浏览器中，某些点击事件失效，经逐行排查，发现是 es6 的问题，所以：
经过此网站 http://ruanyf.github.io/es-checker/index.cn.html 检测后，得出手机端不同浏览器对es6的支持：

1. 华为浏览器  11%
2. UC浏览器  88%
3. QQ浏览器  88%
4. 微信内置浏览器 90%
5. 钉钉内置浏览器  26%

所以，华为浏览器真的坑！

可使用如下网站将 es6 转为 es5 :
https://babeljs.io/repl/#?babili=false&browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=Q&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=true&fileSize=false&timeTravel=false&sourceType=module&lineWrap=false&presets=es2015%2Creact%2Cstage-2&prettier=false&targets=&version=6.26.0&envVersion=


## fixed 定位缺陷

IOS下对元素fixed定位时，若软键盘弹出时，会影响其定位效果，android下fixed表现要比iOS更好，软键盘弹出时，不会影响fixed元素定位 。

解决方案：可用iScroll插件或者better-scroll插件解决这个问题

## 防止图片点击放大预览

1. 只需对不需要进行预览的图片加样式

```
img {
    pointer-events: none;
}
```

2. 图片用背景图的方式插入

```
div {
    background: url(a.png) no repeat center;
}
```

3. 在img元素上添加 onclick="return false", 如下：

```
<img src="***" onclick="return false" />
```
4. js事件阻止默认行为的方法 ----- 有坑！

```
img.addEventListener('click',function(e){

　　e.preventDefault();

});
```
注意：上面的 click 事件在移动端中也可使用 touchend 事件，但是不可使用 touchstart 或 touchmove 事件。

因为，使用 touchstart 或 touchmove 事件后，当页面中上部分有个大图时，当需要滚动页面往下时，是无法滚动的，因为出发了这两个事件。

## 强制修改input中placeholder字体颜色

```
input:-moz-placeholder,
textarea:-moz-placeholder {
    color: #292929;
}

input:-ms-input-placeholder,
textarea:-ms-input-placeholder {
    color: #292929;
}

input::-webkit-input-placeholder,
textarea::-webkit-input-placeholder {
    color: #292929;
}
```
## z-index 在IOS中的缺陷

在IOS系统中，z-index为负数时会失效，所以还是避免负数吧，正数想多大就多大。。。

## iPhoneX 太长

因为 iPhoneX 尺寸太长，导致有些元素在垂向位置不协调，这里只能使用@media媒体查询了：

```
@media all and (max-width: 375px) and (min-height: 750px) {
    .XXX {
        bottom: 4rem;
    }
}
```

## margin-bottom 在苹果手机上无效


当底部有固定导航栏或固定按钮时，主页面会使用margin-bottom或者padding-bottom ， 但是这么做在苹果手机上无法生效，会导致页面无法滑动到底部。

解决办法：在 body 下面添加一个空的 div

```
<div class="margin-bottom-100"></div>
```
```
div.margin-bottom-100 {
    height: 100px;
}

```

## 1px 像素边框的问题

[参考这个](https://caochangkui.github.io/2018/06/28/1px-css/)

## css初始样式重置

```
@charset "utf-8";html{background-color:#fff;color:#000;font-size:12px}
body,ul,ol,dl,dd,h1,h2,h3,h4,h5,h6,figure,form,fieldset,legend,input,textarea,button,p,blockquote,th,td,pre,xmp{margin:0;padding:0}
body,input,textarea,button,select,pre,xmp,tt,code,kbd,samp{line-height:1.5;font-family:tahoma,arial,"Hiragino Sans GB",simsun,sans-serif}
h1,h2,h3,h4,h5,h6,small,big,input,textarea,button,select{font-size:100%}
h1,h2,h3,h4,h5,h6{font-family:tahoma,arial,"Hiragino Sans GB","微软雅黑",simsun,sans-serif}
h1,h2,h3,h4,h5,h6,b,strong{font-weight:normal}
address,cite,dfn,em,i,optgroup,var{font-style:normal}
table{border-collapse:collapse;border-spacing:0;text-align:left}
caption,th{text-align:inherit}
ul,ol,menu{list-style:none}
fieldset,img{border:0}
img,object,input,textarea,button,select{vertical-align:middle}
article,aside,footer,header,section,nav,figure,figcaption,hgroup,details,menu{display:block}
audio,canvas,video{display:inline-block;*display:inline;*zoom:1}
blockquote:before,blockquote:after,q:before,q:after{content:"\0020"}
textarea{overflow:auto;resize:vertical}
input,textarea,button,select,a{outline:0 none;border: none;}
button::-moz-focus-inner,input::-moz-focus-inner{padding:0;border:0}
mark{background-color:transparent}
a,ins,s,u,del{text-decoration:none}
sup,sub{vertical-align:baseline}
html {overflow-x: hidden;height: 100%;font-size: 50px;-webkit-tap-highlight-color: transparent;}
body {font-family: Arial, "Microsoft Yahei", "Helvetica Neue", Helvetica, sans-serif;color: #333;font-size: .28em;line-height: 1;-webkit-text-size-adjust: none;}
hr {height: .02rem;margin: .1rem 0;border: medium none;border-top: .02rem solid #cacaca;}
a {color: #25a4bb;text-decoration: none;}

```

## 未完。。。


