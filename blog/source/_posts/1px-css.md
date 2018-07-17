---
title: 移动端1像素边框问题的解决方案
categories: CSS
tags: [CSS, 移动端]
---

对于不同的移动设备，其物理像素与逻辑像素间存在不同的比例关系。所以我们仅仅在CSS中为border设置1px时，在手机上看起来会显得比较粗，达不到预期效果。

<!-- more -->


## 关于物理像素与逻辑像素

- 物理像素
    移动设备出厂时，不同设备自带的不同像素，也称硬件像素；
- 逻辑像素
    即css中记录的像素。

## 物理像素与逻辑像素的比例

通常可以通过js的 <font color=red >window.devicePixelRatio</font> 在获取不同设备的物理像素和逻辑像素的比例关系（在控制台打印即可得到）。

## 解决 1px 问题的推荐方法

### 方法

项目中引入：border-1px.css，然后通过控制元素的before和after伪元素，改变border大小或颜色。

```
@charset "utf-8";
.border,
.border-top,
.border-right,
.border-bottom,
.border-left,
.border-topbottom,
.border-rightleft,
.border-topleft,
.border-rightbottom,
.border-topright,
.border-bottomleft {
    position: relative;
}
.border::before,
.border-top::before,
.border-right::before,
.border-bottom::before,
.border-left::before,
.border-topbottom::before,
.border-topbottom::after,
.border-rightleft::before,
.border-rightleft::after,
.border-topleft::before,
.border-topleft::after,
.border-rightbottom::before,
.border-rightbottom::after,
.border-topright::before,
.border-topright::after,
.border-bottomleft::before,
.border-bottomleft::after {
    content: "\0020";
    overflow: hidden;
    position: absolute;
}
/* border
 * 因，边框是由伪元素区域遮盖在父级
 * 故，子级若有交互，需要对子级设置
 * 定位 及 z轴
 */
.border::before {
    box-sizing: border-box;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    border: 1px solid #eaeaea;
    transform-origin: 0 0;
}
.border-top::before,
.border-bottom::before,
.border-topbottom::before,
.border-topbottom::after,
.border-topleft::before,
.border-rightbottom::after,
.border-topright::before,
.border-bottomleft::before {
    left: 0;
    width: 100%;
    height: 1px;
}
.border-right::before,
.border-left::before,
.border-rightleft::before,
.border-rightleft::after,
.border-topleft::after,
.border-rightbottom::before,
.border-topright::after,
.border-bottomleft::after {
    top: 0;
    width: 1px;
    height: 100%;
}
.border-top::before,
.border-topbottom::before,
.border-topleft::before,
.border-topright::before {
    border-top: 1px solid #eaeaea;
    transform-origin: 0 0;
}
.border-right::before,
.border-rightbottom::before,
.border-rightleft::before,
.border-topright::after {
    border-right: 1px solid #eaeaea;
    transform-origin: 100% 0;
}
.border-bottom::before,
.border-topbottom::after,
.border-rightbottom::after,
.border-bottomleft::before {
    border-bottom: 1px solid #eaeaea;
    transform-origin: 0 100%;
}
.border-left::before,
.border-topleft::after,
.border-rightleft::after,
.border-bottomleft::after {
    border-left: 1px solid #eaeaea;
    transform-origin: 0 0;
}
.border-top::before,
.border-topbottom::before,
.border-topleft::before,
.border-topright::before {
    top: 0;
}
.border-right::before,
.border-rightleft::after,
.border-rightbottom::before,
.border-topright::after {
    right: 0;
}
.border-bottom::before,
.border-topbottom::after,
.border-rightbottom::after,
.border-bottomleft::after {
    bottom: 0;
}
.border-left::before,
.border-rightleft::before,
.border-topleft::after,
.border-bottomleft::before {
    left: 0;
}
@media (max--moz-device-pixel-ratio: 1.49), (-webkit-max-device-pixel-ratio: 1.49), (max-device-pixel-ratio: 1.49), (max-resolution: 143dpi), (max-resolution: 1.49dppx) {
    /* 默认值，无需重置 */
}
@media (min--moz-device-pixel-ratio: 1.5) and (max--moz-device-pixel-ratio: 2.49), (-webkit-min-device-pixel-ratio: 1.5) and (-webkit-max-device-pixel-ratio: 2.49), (min-device-pixel-ratio: 1.5) and (max-device-pixel-ratio: 2.49), (min-resolution: 144dpi) and (max-resolution: 239dpi), (min-resolution: 1.5dppx) and (max-resolution: 2.49dppx) {
    .border::before {
        width: 200%;
        height: 200%;
        transform: scale(.5);
    }
    .border-top::before,
    .border-bottom::before,
    .border-topbottom::before,
    .border-topbottom::after,
    .border-topleft::before,
    .border-rightbottom::after,
    .border-topright::before,
    .border-bottomleft::before {
        transform: scaleY(.5);
    }
    .border-right::before,
    .border-left::before,
    .border-rightleft::before,
    .border-rightleft::after,
    .border-topleft::after,
    .border-rightbottom::before,
    .border-topright::after,
    .border-bottomleft::after {
        transform: scaleX(.5);
    }
}
@media (min--moz-device-pixel-ratio: 2.5), (-webkit-min-device-pixel-ratio: 2.5), (min-device-pixel-ratio: 2.5), (min-resolution: 240dpi), (min-resolution: 2.5dppx) {
    .border::before {
        width: 300%;
        height: 300%;
        transform: scale(.33333);
    }
    .border-top::before,
    .border-bottom::before,
    .border-topbottom::before,
    .border-topbottom::after,
    .border-topleft::before,
    .border-rightbottom::after,
    .border-topright::before,
    .border-bottomleft::before {
        transform: scaleY(.33333);
    }
    .border-right::before,
    .border-left::before,
    .border-rightleft::before,
    .border-rightleft::after,
    .border-topleft::after,
    .border-rightbottom::before,
    .border-topright::after,
    .border-bottomleft::after {
        transform: scaleX(.33333);
    }
}

```

### 使用案例：

```
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width,user-scalable=no">
    <title> 移动端一像素解决方案 </title>
    <link rel="stylesheet" href="./border-1px.css">
</head>
<style>
    .box {
        padding: 5px;
        margin: 5px;
    }

    .border::before {
        border-color: red;
    }

    .border-top::before {
        border-color: red;
    }

    .border-bottom::before {
        border-color: red;
    }

    .border-topbottom::before,
    .border-topbottom::after {
        border-color: red;
    }

    .border-rightleft::before,
    .border-rightleft::after {
        border-color: red;
    }

    .box2 {
        padding: 5px;
        border: 1px solid red;
    }
</style>

<body>
    <div class="box2">
        <p>这是另一句话，其父元素div的border为没有处理的一像素</p>
    </div>
    <br>
    <div class="box border">
        <p>这是一句话，其父元素div的border为处理后的的一像素</p>
    </div>
    <br>
    <div class="box border-top">
        <p>这是一句话，其父元素div的border-top为处理后的的一像素</p>
    </div>
    <br>
    <div class="box border-bottom">
        <p>这是一句话，其父元素div的border-bottom为处理后的的一像素</p>
    </div>
    <br>
    <div class="box border-topbottom">
        <p>这是一句话，其父元素div的border-topbottom为处理后的的一像素</p>
    </div>
    <br>
    <div class="box border-rightleft">
        <p>这是一句话，其父元素div的border-rightleft为处理后的的一像素</p>
    </div>
</body>

</html>

```



