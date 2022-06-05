---
layout: post
title: engine "node" is incompatible
tags: [Frontend, yarn, Errors]
---

# The engine "node" is incompatible with this module. Expected version XXX

**执行 “yarn install” 报如下错误，错误表示node版本不一致：**

```
error css-loader@1.0.1: The engine "node" is incompatible with this module. Expected version ">= 6.9.0 <7.0.0 || >= 8.9.0". Got "8.1.2"

```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190805095033428.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3l1eGllbGVh,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190805095452915.png)

> **注意：错误报的是Node.js版本不一致，而不是npm版本不一致，所以网上有些建议更新npm的实际上是没用的。**

## 方案1：

卸载旧版[Node](https://so.csdn.net/so/search?q=Node&spm=1001.2101.3001.7020).js，去[官网](https://nodejs.org/en/)下载并重新安装指定版本区间的Node.js后重新执行命令成功：
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/darkchoco10099/img/20190805111242911.png)
忘记Node.js安装位置的可以执行`where node`进行查看：
![在这里插入图片描述](https://cdn.jsdelivr.net/gh/darkchoco10099/img/20190805111814339.png)

## 方案2：

忽略错误后重新`yarn install`

```
 yarn config set ignore-engines true
```