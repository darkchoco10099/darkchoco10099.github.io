---
layout: post
title: Vue项目关闭eslint的方法
subtitle: 简单粗暴好用
tags: [前端开发, Vue]
---

## 方法

在项目[根目录](https://so.csdn.net/so/search?q=根目录&spm=1001.2101.3001.7020)下增加vue.config.js文件。
内容如下：

```javascript
// vue.config.js
module.exports = {
    lintOnSave: false
}
```





出现问题的原因：Eslint的检测机制。
解决方法①：在build/webpack.base.conf.js文件中注释掉第44行代码，如下图，重新yarn start 或者npm run dev

![img](https://img-blog.csdnimg.cn/20190905084526963.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoaXNFcXVhbFRoaXM=,size_16,color_FFFFFF,t_70)

解决方法②：在config/index.js文件中第26行中的useEslint的值改为false，如下图，然后重新启动程序

![img](https://img-blog.csdnimg.cn/20190905085212768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoaXNFcXVhbFRoaXM=,size_16,color_FFFFFF,t_70)



原文链接：https://blog.csdn.net/ThisEqualThis/article/details/100550761