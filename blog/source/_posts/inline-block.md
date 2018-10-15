---
title: 解决 div 设为 inline-block 后标题不对齐
categories: CSS
tags: css
---

vertical-align 属性设置元素的垂直对齐方式。该属性定义行内元素的基线相对于该元素所在行的基线的垂直对齐。允许指定负长度值和百分比值。这会使元素降低而不是升高。在表单元格中，这个属性会设置单元格框中的单元格内容的对齐方式。

<!-- more -->

---

inline-block的默认对齐方式是vertical-block：baseline（基线）。
关于baseline 基线的解释见：[https://www.cnblogs.com/zxjwlh/p/6219896.html](https://www.cnblogs.com/zxjwlh/p/6219896.html)。

可将下面实例中 vertical-align: top; 删除 查看效果变化。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>vertical-align: top;</title>
</head>
<style>
    * {
        margin: 0;
        padding: 0;
    }
    .wrapper {
        width: 500px;
        padding: 0;
        background: #eee;
        margin: 0 auto;
    }
    .item {
        width: 200px;
        padding: 0;
        margin: 20px 23px;
        display: inline-block;
        vertical-align: top;
        text-align: center;
    }
    .box {
        width: 100%;
        height: 300px;
        box-shadow: 0 0 10px #bbb;
    }

    .title {
        word-wrap:break-word;
        font-size: 16px;
        line-height: 1.5;
    }

</style>
<body>
    <div class="wrapper">
        <div class="item">
            <div class="box"> </div>
            <p class="title">短标题</p>
        </div>
        <div class="item">
            <div class="box"> </div>
            <p class="title">这是一个长长长长长长长长长长长长长长长长长长长标题</p>
        </div>
        <div class="item">
            <div class="box"> </div>
            <p class="title">短标题</p>
        </div>
        <div class="item">
            <div class="box"> </div>
            <p class="title">短标题</p>
        </div>
    </div>
</body>
</html>
```


