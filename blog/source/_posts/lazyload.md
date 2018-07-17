---
title: 页面图片懒加载的应用
categories: jQuery
tags: 性能优化
---

当页面中图片较大或者较多时，等待页面载入的时间会很长。此时可以先把img元素或替换成一张占位图，并且使浏览器可视区域外的图片在初始状态下不会被载入，直到用户将页面滚动到它们所在的位置。 这就是图片懒加载，即延迟加载。

<!-- more -->

jquery.lazyload是一个实现图片延迟加载的jQuery 插件，它可以延迟加载长页面中的图片。在浏览器可视区域外的图片在初始状态下不会被载入，直到用户将页面滚动到它们所在的位置。
参考：https://github.com/tuupola/jquery_lazyload/blob/2.x/lazyload.js

```
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width,user-scalable=no">
    <title>懒加载</title>
</head>

<body>
    <img src="https://iph.href.lu/200x200?text=占位图片" src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://github.com/caochangkui/demo/blob/master/some-demo/avator_m.jpg?raw=true"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>
    <img src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://github.com/caochangkui/demo/blob/master/some-demo/avator_m.jpg?raw=true"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>

    <img src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1528170241798&di=ff6ad270689d6b8a6703427e4a98e675&imgtype=0&src=http%3A%2F%2Fimgsrc.baidu.com%2Fimgad%2Fpic%2Fitem%2F5bafa40f4bfbfbed77eb0e6c72f0f736afc31f76.jpg"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>

    <img src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1528170241797&di=e5643174b876c65c9e8b8e3eda08c001&imgtype=0&src=http%3A%2F%2Fimgsrc.baidu.com%2Fimgad%2Fpic%2Fitem%2F32fa828ba61ea8d35e5c44059d0a304e251f58b0.jpg"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>

    <img src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1528170342150&di=7f9be24d1a7918dbe89ef903eccd42ca&imgtype=0&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01f55e56b29d6032f875520fef9af9.jpg%401280w_1l_2o_100sh.jpg"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>

    <img src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1528170342433&di=4c9c7087b50da1f46b81e114973330d4&imgtype=0&src=http%3A%2F%2Fwww.cnr.cn%2Fnewscenter%2Fnative%2Fgd%2F20180117%2FW020180117368234306480.jpg"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>

    <img src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1528170342433&di=598ee5a98e063ff8ead0b60795ec2c46&imgtype=0&src=http%3A%2F%2Fstatic01.lvye.com%2Fforum%2F201602%2F03%2F111456et22rgkaszjt55sz.jpg"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>

    <img src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1528170342432&di=02bffef718b9125ebdac3b4bd37ae9b3&imgtype=0&src=http%3A%2F%2Fyouimg1.c-ctrip.com%2Ftarget%2F100a060000001gghm67FA.jpg"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>

    <img src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1528170342432&di=dbd01415e716798aa8b3c0e70218c667&imgtype=0&src=http%3A%2F%2Fyouimg1.c-ctrip.com%2Ftarget%2Ffd%2Ftg%2Fg4%2FM09%2FA0%2F3C%2FCggYHFaK7aSAFlRoAAG0XA9t9W4330.jpg"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>

    <img src="https://iph.href.lu/200x200?text=占位图片" class="lazyload" alt="" width="200" height="140" data-original="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1528170342430&di=1761ea2e8228b9fc940ce7a55540f9b6&imgtype=0&src=http%3A%2F%2Fimgsrc.baidu.com%2Fimage%2Fc0%253Dshijue1%252C0%252C0%252C294%252C40%2Fsign%3Db9500cccf8d3572c72ef949fe27a0952%2F10dfa9ec8a136327d15199169b8fa0ec08fac753.jpg"/>
    <br> <br> <br> <br> <br>  <br> <br> <br> <br> <br> <hr>

</body>
<script src="jquery.js"></script>
<script src="jquery.lazyload.js"></script>
<script>
    $(function () {
        $("img.lazyload").lazyload({})
    });
</script>

</html>
```

