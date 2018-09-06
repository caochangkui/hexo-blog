---
title: 华为手机自带浏览器不支持 ES6 语法
categories: 移动端
tags: ES6
---

华为手机自带浏览器对 es6 语法的支持度极差，哪怕最新的荣耀10 手机也有该毛病！所以，移动端项目开发中，发布前最好将所有的 es6 语法转为 es5。

<!-- more -->

---

真机测试时，发现在华为手机自带浏览器中，某些点击事件失效，经逐行排查，发现是 es6 的问题。
经过此网站 http://ruanyf.github.io/es-checker/index.cn.html 检测后，得出手机端不同浏览器对es6的支持：

1. 华为浏览器  11%
2. UC浏览器  88%
3. QQ浏览器  88%
4. 微信内置浏览器 90%
5. 钉钉内置浏览器  26%

所以，华为浏览器真的坑！如果某 js 文件中使用了 es6 语法，真个 js 文件都是无效的！！！

可使用如下网站将 es6 转为 es5 :
https://babeljs.io/repl/#?babili=false&browsers=&build=&builtIns=false&spec=false&loose=false&code_lz=Q&debug=false&forceAllTransforms=false&shippedProposals=false&circleciRepo=&evaluate=true&fileSize=false&timeTravel=false&sourceType=module&lineWrap=false&presets=es2015%2Creact%2Cstage-2&prettier=false&targets=&version=6.26.0&envVersion=

