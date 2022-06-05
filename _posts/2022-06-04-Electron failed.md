---
​---
layout: post
title: Electron failed
tags: [Frontend, npm, Errors]
​---
---

# Electron failed to install correctly, please delete node_modules/electron and try installing again

出于兴趣，跑下electron的官方demo，一直出现Electron failed to install correctly, please delete node_modules/electron and try installing again；困扰了许久。尝试过重装npm和给npm配置淘宝镜像，都无果之后在github上找到答案。

问题原因
主要是因为在install的时候node_modules/electron/ 中文件的丢失造成程序无法执行。对比下图很明显发现少了path.txt和dist文件夹。

缺失的electron文件：

正常的electron文件：


解决方案
要重新安装加载electron。这只是其中一个解决方案。参考https://github.com/pangxieju/electron-fix

首先 npm instal或者yarn install
执行 npm install electron-fix -g
接着 electron-fix start
然后在package.json的scripts加入
```
"scripts": {
  "fix": "electron-fix start"
}
```
执行 npm run fix
最后再 npm start 或者 yarn start 一下就成功了，终于舒服了
原文链接：https://blog.csdn.net/qq_42789068/article/details/106401830