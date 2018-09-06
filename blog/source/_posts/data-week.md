---
title: JS 精确获取每月有几周（每周五到周四算作一周）
categories: JavaScript
tags: [JavaScript, Data]
---

将每周五至周四算作一周，计算每月有几周，并获取到每周的起始时间。

<!-- more -->
## 日期格式化

```
Date.prototype.format = function (fmt) {
    var o = {
        "M+": this.getMonth() + 1, //月份
        "d+": this.getDate(), //日
        "h+": this.getHours(), //小时
        "m+": this.getMinutes(), //分
        "s+": this.getSeconds(), //秒
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度
        "S": this.getMilliseconds() //毫秒
    };
    if (/(y+)/.test(fmt)) {
        fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    }
    for (var k in o) {
        if (new RegExp("(" + k + ")").test(fmt)) {
            fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
        }
    }
    return fmt;
}
```
## 函数 allWeeks 得到指定月份的各周真实日期

```
// 本月的每一周（从上周五到本周四为一周）
function allWeeks(now_month) {
    let week_array = [];
    let today = new Date(Date.parse(now_month));
    let year = today.getFullYear();
    let month = today.getMonth();
    let i = 0;

    let start = new Date(year, month, 1); // 得到当月第一天
    let end = new Date(year, month+1, 0); // 得到当月最后一天
    let start_day = start.getDay(); // 当月第一天是周几
    console.log(start.format("yyyy-MM-dd"), end.format("yyyy-MM-dd")); // 每月的起始日期
    switch(start_day)
    {
        case 0: i = 0 - 1; break;
        case 1: i = 0 - 2; break;
        case 2: i = 0 - 3; break;
        case 3: i = 0 - 4; break;
        case 4: i = 0 - 5; break;
        case 5: i = 1; break;
        case 6: i = 0; break;
    }

    while ( new Date(year, month, i + 6) <= end) {

        week_array.push([  new Date(year, month, i).format("yyyy-MM-dd"),
                           new Date(year, month, i + 6).format("yyyy-MM-dd")
                        ]
                    )
        i += 7;
    }

    console.log(week_array);
    return week_array;
}

```
## 例如

allweeks('2018-08');

结果：
```
第一周：["2018-07-27", "2018-08-02"]
第二周：["2018-08-03", "2018-08-09"]
第三周：["2018-08-10", "2018-08-16"]
第四周：["2018-08-17", "2018-08-23"]
第五周：["2018-08-24", "2018-08-30"]
```

allweeks('2018-07');

结果：
```
第一周：["2018-06-29", "2018-07-05"]
第二周：["2018-07-06", "2018-07-12"]
第三周：["2018-07-13", "2018-07-19"]
第四周：["2018-07-20", "2018-07-26"]
```