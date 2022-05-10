---
layout: post
title: Django与Vue的连接与开发
subtitle: 详细介绍了如果前后端分离的开发python web应用
tags: [python, 全栈开发, Django, Vue]
---

- 原文链接：[我如何使用 Django + Vue.js 快速构建项目 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/24893786)
- 原文链接：[整合 Django + Vue.js 框架快速搭建web项目 - 云+社区 - 腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1005607)
- 原文链接：[(61条消息) 记录Django API与Vue前端进行交互_花想容~Bxy的博客-CSDN博客_vue和django交互](https://blog.csdn.net/qq_42992704/article/details/105869676)



小节：django如何从html页面从取值？

1. 首先需要通过URL传值：http://127.0.0.1:8000/delete_user/?name='张三'&id=7　　　　　　//这个URL就可以达到传值的效果

2.看html文件上的form标签的method是post还是get方法。

然后通过request对象以及HTML文件上form标签里面的别的标签的name对应值再取值。如下：

如果是post请求：

new_id = request.POST.get(id=7, None)

如果是get请求:

new_id = request.GET.get(id=7, None)

3.接着就是可以通过获得到的new_id值进行各种操作，例如，通过ORM对数据表上的 增、删、改、查等
————————————————
版权声明：本文为CSDN博主「杂志社社内刘编辑」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_36034659/article/details/111904741