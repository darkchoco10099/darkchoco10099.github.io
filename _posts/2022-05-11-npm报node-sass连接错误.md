---
layout: post
title: npm报node-sass连接错误
tags: [Errors, node]
---

1、在进行npm install时报错    如果软件[node](https://so.csdn.net/so/search?q=node&spm=1001.2101.3001.7020).js版本没问题的话   执行npm install时报如下错误

![](https://cdn.jsdelivr.net/gh/darkchoco10099/img/202205112150508.png)

2、报错原因

是因为[sass](https://so.csdn.net/so/search?q=sass&spm=1001.2101.3001.7020)安装源的问题 修改sass安装源就能解决问题，使用命令：

npm config set sass\_binary\_site=https://npm.taobao.org/mirrors/node-sass

![](https://cdn.jsdelivr.net/gh/darkchoco10099/img/202205112150476.png)

3、在运行npm install就能运行成功

![](https://cdn.jsdelivr.net/gh/darkchoco10099/img/202205112150705.png)