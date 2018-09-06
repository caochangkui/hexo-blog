---
title: HTML 中使 footer 始终处于页面底部
categories: CSS
tags: css
---

通常在页面中，需要使页脚 footer 部分始终处于底部。当页面高度不够 100% 时， footer 处于页面最底部，当页面内容高于 100% 时，页脚元素可以被撑到最底部。

<!-- more -->
## 方法一：绝对定位

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>旋转六面体动画</title>
    <style>
        * {
            padding: 0;
            margin: 0;
            box-sizing: border-box;
        }

        html {
            height: 100%
        }
        /* 这里footer的父元素为 body, 实际应用中，不一定要以body为父元素，只要确保footer的父元素的最小高度为100%就行 */
        body {
            position: relative;
            min-height: 100%;
            padding: 0;
            padding-bottom: 40px;
        }

        #footer {
            height: 40px;
            background: #eee;
            width: 100%;
            position: absolute;
            bottom: 0;
        }
    </style>
</head>

<body>
    <div class="box">
        <h1>content</h1>
        <h1>content</h1>
        <h1>content</h1>
        <h1>content</h1>
        <h1>content</h1>
    </div>
    <footer id="footer">
        <p>footer footer footer</p>
    </footer>
</body>

</html>

```

### 方法二: flex 布局

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>footer</title>
    <style>
        * {
            padding: 0;
            margin: 0;
            box-sizing: border-box;
        }

        html {
            height: 100%
        }

        body {
            height: 100%;
            display: flex;
            flex-direction: column;
        }

        #header {
            height: 40px;
            background: red;
            flex: 0 0 auto;
        }

        #box {
            background: #eee;
            flex: 1 0 auto;
        }

        #footer {
            height: 40px;
            background: rgb(129, 129, 201);
            flex: 0 0 auto;
        }
    </style>
</head>

<body>
    <header id="header">
        header header header
    </header>
    <div id="box">
        <h1>content</h1>
        <h1>content</h1>
        <h1>content</h1>
        <h1>content</h1>
        <h1>content</h1>
    </div>
    <footer id="footer">
        <p>footer footer footer</p>
    </footer>
</body>

</html>

```
