---
title: 原生 JS 实现手机验证码倒计时
categories: JavaScript
tags: [JS, CSS]
---

可以使用 pointer-events 来阻止元素成为鼠标事件的 target。html5 新增操作元素 class 类名的方式 classList。

<!-- more -->
## classList 方法

- add(value)：在元素中添加一个或多个类名。如果值已经存在，就不添加了。
- contains(value): 返回布尔值，判断指定的类名是否存在。
- remove(value)：移除元素属性列表中一个或多个类名。注意： 移除不存在的类名，不会报错。
- toggle(value)：在元素中切换类名。如果列表中已经存在给定的值，删除它；如果列表中没有给定的值，添加它

## 原生 JS 实现手机验证码倒计时

单击“发送验证码”后，需等待 10 秒才能再次单击“重发获取”，在此期间，可以使用 pointer-events 来阻止元素成为鼠标事件的目标。源码参考如下。

```
<!DOCTYPE html>
<html>

<head>
    <title> 手机验证码 </title>
    <meta charset="utf-8" />
</head>

<style>
    a{
        color:red;
    }
    .disable{
        pointer-events:none;
        color:#666;
    }
</style>

<body>
    <p>
        <input type="text" placeholder="请输入手机号">
    </p>
    <p>
        <input type="text" placeholder="验证码">
        <a href="javascript:;" id="btn">发送验证码</a>
    </p>


    <script type="text/javascript">
        var oBtn = document.getElementById('btn');
        var flag = true;

        oBtn.addEventListener("click", function () {
            var time = 10;
            oBtn.classList.add('disable');
            oBtn.innerText = '已发送';

            if (flag) {
                flag = false;
                var timer = setInterval(() => {
                    time--;
                    oBtn.innerText = time + ' 秒';
                    if (time === 0) {
                        clearInterval(timer);
                        oBtn.innerText = '重新获取';
                        oBtn.classList.remove('disable');
                        flag = true;
                    }
                }, 1000)
            }
        });

    </script>
</body>

</html>

```