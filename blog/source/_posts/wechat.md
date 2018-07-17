---
title: 基于Vue.js 2.× + Vuex打造微信项目
categories: Vue
tags: [Vue, 移动端]
---

基于Vue + Vuex + Vue-router + Webpack 2.0打造微信界面，实现了微信聊天、搜索、点赞、通讯录（快速导航）、个人中心、模拟对话、朋友圈、设置等功能。

<!-- more -->
## 一、项目简介

基于Vue + Vuex + Vue-router + Webpack 2.0打造微信界面，实现了微信聊天、搜索、点赞、通讯录（快速导航）、个人中心、模拟对话、朋友圈、设置等功能。

## 二、项目预览 （请在chrome手机模式下打开）

[点击这里预览项目](https://caochangkui.github.io/MyItems/wechat-by-cck/index.html)


### 移动端扫描下方二维码可直接打开

![](http://images.cnblogs.com/cnblogs_com/cckui/1071419/o_1530259424.png)



## 三、技术栈


- MVVM框架：Vue.js 2.0
- 状态管理：Vuex
- 移动端组件库：Mint-ui
- 前端路由：Vue-router
- 数据交互：Vue-resource
- 打包工具：webpack 2.0
- 环境配置：node + npm
- 语言：es6


## 四、项目运行

```
git clone https://github.com/caochangkui/wechat-by-vue.git

cd wechat-by-vue

npm install

npm run dev //服务端运行，运行后访问 http://localhost:6868)

npm run build //项目打包

```


## 五、页面部分截图

### 1. 微信聊天（每个联系人聊天后可自动添加到首页）

<img src="http://images.cnblogs.com/cnblogs_com/cckui/1069317/o_GIF111.gif" width="225" height="400"  />


### 2.朋友圈、点赞

<img src="http://images.cnblogs.com/cnblogs_com/cckui/1069317/o_GIF222.gif" width="225" height="400" />

### 3.个人中心、相册、钱包、卡包、设置

<img src="http://images.cnblogs.com/cnblogs_com/cckui/1069317/o_GIF333.gif" width="225" height="400" />



## 六、项目树
```
.
├── README.md
├── build                                              // 项目打包路径
│   ├── build.js
│   ├── check-versions.js
│   ├── dev-client.js
│   ├── dev-server.js
│   ├── utils.js
│   ├── vue-loader.conf.js
│   ├── webpack.base.conf.js
│   ├── webpack.dev.conf.js
│   └── webpack.prod.conf.js
├── config                                            // 上线项目文件
│   ├── dev.env.js
│   ├── index.js
│   └── prod.env.js
├── index.html
├── package.json                                      // 配置信息
└── src                                               // 源码目录
    ├── App.vue                                       // 输出文件
    ├── main.js                                       // 入口文件
    ├── assets                                        // 公用图片
    ├── base                                          // 存放通用组件的组件库
    │   ├── loading                                   // 栏加载组件
    │   └── scroll                                    // 滑屏文件
    ├── components                                    // 应用组件的组件库
    │   ├── chat
    │   │   └── chat.vue                              // 微信组件
    │   ├── address
    │   │   └── address.vue                           // 通讯录组件
    │   │   └── address-detail
    │   │       └── address-detail.vue                // 通讯录详情组件
    │   │       └── address-more
    │   │           └── address-more.vue              // 通讯录更多详情组件
    │   ├── find
    │   │   ├── find.vue                              // 发现组件
    │   │   ├── find-circle
    │   │   │   └── find-circle.vue                   // 朋友圈组件
    │   │   ├── scan
    │   │   │   └── scan.vue                          // 扫一扫组件
    │   │   └── shake
    │   │       └── shake.vue                         // 摇一摇组件
    │   ├── me
    │   │   ├── me.vue                                // 个人中心组件
    │   │   ├── card
    │   │   │   └── card.vue                          // 卡包组件
    │   │   ├── money
    │   │   │   └── money.vue                         // 钱包组件
    │   │   ├── collection
    │   │   │   └── collection.vue                    // 收藏组件
    │   │   ├── album
    │   │   │   └── album.vue                         // 相册组件
    │   │   └── set
    │   │       └── set.vue                           // 设置组件
    │   ├── chatroom
    │   │   └── chatroom.vue                          // 聊天窗口组件
    │   │   └── chatroom-user
    │   │       └── chatroom-user.vue                 // 聊天者的个人信息组件
    │   ├── search
    │   │   └── search.vue                            // 搜索组件
    │   ├── plus
    │   │   └── plus.vue                              // 更多组件
    ├── router
    │   └── index.js                                  // 路由控制中心
    └── store                                         //  存放vuex相关代码
        ├── actions.js                                //  异步操作，或对mutation做一些封装
        ├── getters.js                                //  获取state，并对其做一些映射
        ├── index.js                                  // vuex入口文件
        ├── mutation-types.js                         // 存放与mutatiom相关的常量
        ├── mutations.js                              //  处理数据逻辑方法的集合
        └── state.js                                  //  管理所有状态


```


