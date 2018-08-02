---
title: 修改 input[type="radio"] 和 input[type="checkbox"] 的默认样式
categories: CSS
tags: [css, input]
---

表单中，经常会使用到单选按钮和复选框，但是，input[type="radio"] 和 input[type="checkbox"] 的默认样式在不同的浏览器或者手机上，显示的效果总是不统一，而且难以修改器样式。

<!-- more -->
## input[type="radio"] 样式定制


代码：

```
<form>
    <p>
        <input type="radio" name="gender" id="male" value="male">
        <label for="male">男士</label>
    </p>
    <p>
        <input type="radio" name="gender" id="female" value="female">
        <label for="female">女士</label>
    </p>
</form>
```
css 样式

```
input[type="radio"] {
	height: 22px;
	width: 22px;
	margin-right: 10px;
	display: none;
}
input[type="radio"] + label::before {
    content: "\a0"; /*不换行空格*/
    display: inline-block;
    vertical-align: middle;
    font-size: 18px;
    width: 18px;
    height: 18px;
    margin-right: 10px;
    border-radius: 50%;
	border: 1px solid #003c66;
	background: #fff;
	line-height: 22px;
	box-sizing: border-box;
}
input[type="radio"]:checked + label::before {
    background-color: #003c66;
    background-clip: content-box;
    padding: 3px;
}

```


效果如图：

![单选框](https://github.com/caochangkui/demo/blob/master/some-demo/radio.jpg?raw=true)

## input[type="checkbox"] 样式定制

代码：

```
<form>
    <input id="select_all" name="select_all" type="checkbox">
    <label for="select_all"> <i></i>选择</label>
</form>
```
css 样式

```
input[type="checkbox"] {
    display: none;
}

input[type="checkbox"]+label>i {
    display: inline-block;
    width: 20px;
    height: 20px;
    border: 1px solid #bbb;
    background: #bbb;
    margin-right: 10px;
    vertical-align: middle;
}

input[type="checkbox"]:checked+label>i {
    position: relative;
}

input[type="checkbox"]:checked+label>i::before {
    content: '';
    position: absolute;
    width: 12px;
    height: 18px;
    color: black;
    border-bottom: 1px solid green;
    border-right: 1px solid green;
    left: 50%;
    top: 20%;
    transform-origin: center;
    transform: translate(-50%, -30%) rotate(40deg);
    -webkit-transform: translate(-50%, -30%) rotate(40deg);
}
```

效果如图：

![复选框](https://github.com/caochangkui/demo/blob/master/some-demo/checkbox.jpg?raw=true)