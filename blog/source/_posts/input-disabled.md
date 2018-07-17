---
title: 表单设置 disabled 后无法传值到后台的解决办法
categories: HTML
tags: form表单
---

在提交 from 表单时，下面的 input 无法正常提交给后台， 发现，如果input的字段设为disabled，该表单是无法提交的。

<!-- more -->

```
<input type="text" name="name" disabled />
```

## 解决方法

1. 将表单中字段 disabled 用 readonly 代替即可（如有需要，可以对该表单加上灰色的背景色）
2. 可以在写一个隐藏属性，一个用于传值，一个用于显示

## disabled和readonly的异同

### 相同点

- 都可使文本框不能输入文字。
- 可以通过js脚本修改其value值。
- 想要撤销，只能删除相应的属性，设置flase无效

### 不同点

#### disabled

- input无法接收焦点
- 使用tab键会跳过元素
- disabled不会对任何事件进行响应（比如：click事件无效）。
- disabled的元素的值不会提交。
- disabled属性可以用于所有的表单元素。

#### readonly

- input可以接收焦点
- 使用tab键不会跳过元素
- readonly会对事件进行响应。
- readonly的元素的值会提交。
- readonly属性只对 type="text" 、 textarea 和 type="password" 有效。

