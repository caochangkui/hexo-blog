---
title: 屏幕视口宽度及元素尺寸的获取
categories: CSS
tags: [CSS, JavaScript, jQuery]
---

原生 JavaScript 和 jQuery 获取屏幕视口宽度及元素尺寸的方法：

<!-- more -->

## 屏幕视口宽度
```
// 原生js方法:
window.innerHeight  // 标准浏览器及IE9+
document.documentElement.clientHeight  // 标准浏览器及低版本IE标准模式
document.body.clientHeight  // 低版本混杂模式

// jQuery方法：
$(window).height()
```
## 滚动条滚动的距离

获取浏览器窗口顶部与文档顶部之间的距离，即滚动条滚动的距离

```
// 原生js方法：
window.pagYoffset  // 标准浏览器及IE9+
document.documentElement.scrollTop  // 兼容ie低版本的标准模式
document.body.scrollTop  // 兼容混杂模式
// jQuery方法：
$(document).scrollTop()
```

## 获取元素尺寸

```
<body>
    <div id="box" style="height: 100px; width: 100px; border: 1px solid #bbb; padding: 10px; margin: 15px;"> </div>
</body>
```

```
let box = document.getElementById('box');

$('#box').width() = el.style.width;
$('#box').innerWidth() = el.style.width+el.style.padding;
$('#box').outerWidth() = el.offsetWidth = el.style.width+el.style.padding+el.style.border；
$('#box').outerWidth(true) = el.style.width+el.style.padding+el.style.border+el.style.margin；

```
但是，如果像上面使用原生style.xxx方法获取属性，这个元素必须已经有内嵌的样式，即`<div style="...."></div>`；

如果原先是通过外部或内部样式表定义css样式，必须使用`window.getComputedStyle("元素", "伪类")[xxx]`来获取样式值。

可以参考[：获取元素CSS值之getComputedStyle方法熟悉--张鑫旭 ](https://www.zhangxinxu.com/wordpress/2012/05/getcomputedstyle-js-getpropertyvalue-currentstyle/)


## 获取元素的位置
```
// 原生js方法：
object.getBoundingClientRect(); // 返回元素的大小及其相对于视口的位置
// jQuery方法：
$(object).offset().top;   // 元素距离文档顶距离
$(object).offset().left;   //元素距离文档左边距离。
```


## 获取页面滚动位置


如果已定义，请使用pageXOffset和pageYOffset，否则使用scrollLeft和scrollTop，可以省略el来使用window的默认值。

```
const getScrollPos = (el = window) =>

  ({x: (el.pageXOffset !== undefined) ? el.pageXOffset : el.scrollLeft,

    y: (el.pageYOffset !== undefined) ? el.pageYOffset : el.scrollTop});

// getScrollPos() -> {x: 0, y: 500}
```

## 页面平滑滚动到顶部

使用document.documentElement.scrollTop或document.body.scrollTop获取到顶部的距离。
从顶部滚动一小部分距离。
使用window.requestAnimationFrame（）来滚动。
```
const scrollToTop = () => {
  const c = document.documentElement.scrollTop || document.body.scrollTop;
  if (c > 0) {
    window.requestAnimationFrame(scrollToTop);
    window.scrollTo(0, c - c / 8);
  }

};

// scrollToTop();
```