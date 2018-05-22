#### hexo-blog
---
## install hexo
```
$ npm install -g hexo-cli
```

## init
```
$ hexo init blog
```

## generetor
```
$ cd blog
$ hexo g
```

## server
```
$ hexo s
```

## 主题

https://hexo.io/themes/

#### next 主题有三种选择, 根目录/themes/next/_congig.yml 文件中修改

Muse - 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
Mist - Muse 的紧凑版本，整洁有序的单栏外观
Pisces - 双栏 Scheme， 清新

## 写文章

/source/_posts下创建文章

## 本地测试
$ hexo s
测试服务启动，你可以在浏览器中输入https://localhost:4000 访问

## 通过安装hexo-deployer-git自动部署发布工具

```
$ npm install hexo-deployer-git --save
```

## 发布

测试没问题后，可以通过下面命令发布到github上

```
$ hexo clean && hexo g && hexo d
```




