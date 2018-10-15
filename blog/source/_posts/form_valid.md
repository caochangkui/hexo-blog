---
title: jQuery Validate 表单验证实例
categories: jQuery
tags: [JS, jQuery]
---

jQuery Validate 插件功能丰富，使用简单，可以在页面中很方便的用作表单验证。

<!-- more -->
## 实例如下

```
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <title>表单验证</title>

    <style>
        .error{
            color:red;
        }
    </style>
</head>

<body>
    <form class="cmxform" id="signupForm" method="get" action="">
        <fieldset>
            <legend>验证完整的表单</legend>
            <p>
                <label for="firstname">名字</label>
                <input id="firstname" name="firstname" type="text">
            </p>
            <p>
                <label for="username">用户名</label>
                <input id="username" name="username" type="text" required minlength="2">
            </p>
            <p>
                <label for="password">密码</label>
                <input id="password" name="password" type="password">
            </p>
            <p>
                <label for="confirm_password">验证密码</label>
                <input id="confirm_password" name="confirm_password" type="password">
            </p>
            <p>
                <label for="email">Email</label>
                <input id="email" name="email" type="email">
            </p>
            <p>
                <label for="agree">请同意我们的声明</label>
                <input type="checkbox" class="checkbox" id="agree" name="agree">
            </p>
            <p>
                <label for="newsletter">我乐意接收新信息</label>
                <input type="checkbox" class="checkbox" id="newsletter" name="newsletter">
            </p>
            <p>
                <input class="submit" type="submit" value="提交">
            </p>
        </fieldset>
    </form>

    <script src="./jquery.min.js"></script>
    <script src="./jquery.validate.min.js"></script>
    <script src="./messages_zh.js"></script>
    <script>
        $().ready(function () {
            // 在键盘按下并释放及提交后验证提交表单
            $("#signupForm").validate({
                // 表单验证规则（也可直接写在html元素标签中）
                rules: {
                    firstname: "required",
                    password: {
                        required: true,
                        minlength: 5
                    },
                    confirm_password: {
                        required: true,
                        minlength: 5,
                        equalTo: "#password"
                    },
                    email: {
                        required: true,
                        email: true
                    },
                    "topic[]": {
                        required: "#newsletter:checked",
                        minlength: 2
                    },
                    agree: "required"
                },
                // 表单错误时的提示信息，如果不写，则调用默认信息（在messages_zh.js）
                messages: {
                    firstname: "请输入您的名字",
                    username: {
                        required: "请输入用户名",
                        minlength: "用户名必需由两个字母组成"
                    },
                    password: {
                        required: "请输入密码",
                        minlength: "密码长度不能小于 5 个字母"
                    },
                    confirm_password: {
                        required: "请输入密码",
                        minlength: "密码长度不能小于 5 个字母",
                        equalTo: "两次密码输入不一致"
                    },
                    email: "请输入一个正确的邮箱",
                    agree: "请接受我们的声明",
                    topic: "请选择两个主题"
                },
                // submitHandler：通过验证后运行的函数，里面要加上表单提交的函数，否则表单不会提交。
                submitHandler: function (form) {
                    alert("提交事件!");
                }
            });
        });
    </script>
</body>

</html>

```

## 参考

- http://www.runoob.com/jquery/jquery-plugin-validate.html
- https://github.com/jquery-validation/jquery-validation