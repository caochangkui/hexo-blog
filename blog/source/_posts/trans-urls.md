---
title: 使用新浪 API 将一个或多个长链接转换成短链接
categories: JavaScript
tags: JavaScript
---

使用新浪短网址接口可以很方便的将一个或者多个长链接短程短连接。

<!-- more -->
## 新浪开放平台

参考开发文档：http://open.weibo.com/wiki/2/short_url/shorten


## 请求示例

```
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>短连接</title>
</head>
<style>
    input {
        height: 20px;
        width: 200px;
    }
</style>
<body>
    <div id="box">
        <form action="">
            <label for="url_long">长链接</label>
            <input type="text" placeholder="长链接" id="url_long">
            <br>
            <br>
            <label for="url_long">短链接</label>
            <input type="text" placeholder="短链接" id="short_long">
            <br>
            <br>
            <button type="button" id="btn">转换</button>
        </form>
    </div>

    <script> https://cdn.bootcss.com/jquery/3.3.1/jquery.min.js</script>
    <script>
        $(document).ready(function () {

            var source = '4007171625';
            $('#btn').click(function () {
                var response_data = '';
                var url_long = $('#url_long').val();
                var url = `https://api.weibo.com/2/short_url/shorten.json?url_long=${url_long}&source=4007171625`;
                $.ajax({
                    url: url,
                    type: 'GET',
		            async: false,
                    dataType: 'jsonp',
                    crossDomain: true,
                    success: function (data) {
                        console.log(data);
                        response_data = data.data.urls[0].url_short;
                        console.log(response_data)
                        $('#short_long').val(response_data)
                    },
                    error: function (response) {
                        console.log('请求出错--->', response);
                    }
                });
            })
        });
    </script>
</body>

</html>

```