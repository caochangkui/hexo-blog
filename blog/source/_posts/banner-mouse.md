---
title: banner 跟随鼠标呈现视差效果
categories: JavaScript
tags: css
---

参考 Element 官网，利用 js / jq 和 css3， 实现某图片随着鼠标移动呈现的视差效果。

<!-- more -->

---


```
<!DOCTYPE html>
<html>

<head>
    <title>水波背景</title>
    <meta charset="utf-8" />
    <style>
        * {
            transition: all .3s;
        }

        .perspective {
            perspective: 800px;
        }

        .preserve3d {
            position: relative;
            width: 500px;
            height: 400px;
            margin: 160px auto;
            background: #4b5cce url("http://data.banyanbbt.org/static/newimg/top/right.png") center no-repeat;
            background-size: 100% 100%;
            border-radius: 20px;
            transform-style: preserve-3d;
        }
    </style>
</head>

<body>
    <div class="perspective">
        <div class="preserve3d">
        </div>
    </div>

    <script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.js"></script>
    <script type="text/javascript">

        /* 原生js实现 */

        (function () {
            var imgPX = 0;
            var imgPY = 0;
            var divWidth = 0;
            var divHeight = 0;
            var flag = false; // 记录鼠标是否按下

            var preserve3d = document.querySelector(".preserve3d");

            console.log(preserve3d.offsetLeft, preserve3d.offsetTop)
            console.log(preserve3d.clientWidth, preserve3d.clientHeight)

            preserve3d.addEventListener("mouseenter", function (e) {
                flag = true;
                var evt = e || window.event;
                imgPX = preserve3d.offsetLeft;
                imgPY = preserve3d.offsetTop;
                divWidth = preserve3d.clientWidth;
                divHeight = preserve3d.clientHeight;

                document.addEventListener("mousemove", function (e) {
                    if (flag) {
                        var evt = e || window.event;
                        var mouseX = evt.clientX - imgPX;
                        var mouseY = evt.clientY - imgPY;
                        var X = mouseX - divWidth / 2;
                        var Y = divHeight / 2 - mouseY;
                        preserve3d.style.transform =
                            `rotateY(${ X / 20 }deg) rotateX(${ Y / 20 }deg)`
                    }
                });

                document.addEventListener("mouseout", function () {
                    flag = false;
                    preserve3d.style.transform = `rotateY(${ 0 }deg) rotateX(${ 0 }deg)`
                    document.removeEventListener("mouseout", function () {
                        flag = false;
                    });
                })

            });
        })();


        /* jq 实现 */

        // (function () {
        //     var imgPX = 0;
        //     var imgPY = 0;
        //     var divWidth = 0;
        //     var divHeight = 0;

        //     $('.preserve3d').on('mouseenter', function () {
        //         imgPX = $(this).offset().left;
        //         imgPY = $(this).offset().top;
        //         divWidth = $(this).outerWidth();
        //         divHeight = $(this).outerHeight();

        //         console.log($(this).offset().left, $(this).offset().top)

        //     }).on('mousemove', function (event) {
        //         var mouseX = event.pageX - imgPX;
        //         var mouseY = event.pageY - imgPY;
        //         var X = mouseX - divWidth / 2;
        //         var Y = divHeight / 2 - mouseY;
        //         $(this).css({
        //             "transform": "rotateY(" + X / 20 + "deg) " + "rotateX(" + Y / 20 + "deg) "
        //         });
        //     }).on('mouseleave', function () {
        //         $(this).css({
        //             "transform": "rotateY(0deg) rotateX(0deg)"
        //         })
        //     })
        // })();
    </script>
</body>

</html>
```


