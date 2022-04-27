---
layout: post
title: YAML Front 头信息相关配置
subtitle: 整理YAML头信息相关内容（持续更新）
cover-img: /assets/img/path.jpg
tags: [YAML, 持久积累]
---

通过这个文章收集YAML头信息的相关用法，并结合此Jekyll进行更好的显示，长期积累项目。

正是头信息开始让 Jekyll 变的很酷。任何只要包含 [YAML](http://yaml.org/) 头信息的文件在 Jekyll 中都能被当做一个特殊的文件来处理。头信息必须在文件的开始部分，并且需要按照 YAML 的格式写在两行三虚线之间。下面是一个基本的例子：

```YAML
---
layout: post
title: Blogging Like a Hacker
---
```

在这两行的三虚线之间，你可以设置预定义的变量（下面这个例子可以作为参考），甚至创建一个你自己定义的变量。这样在接下来的文件和任意模板中或者在包含这些页面或博客的模板中都可以通过使用 Liquid 标签来访问这些变量。

## 预定义的全局变量[Permalink](https://darkchoco10099.github.io/2022-04-27-YAML_Front/#预定义的全局变量)

你可以在页面或者博客的头信息里设置这些已经预定义好的全局变量。

| 变量名称    | 描述                                                         |
| ----------- | ------------------------------------------------------------ |
| `layout`    | 如果设置的话，会指定使用该模板文件。指定模板文件时候不需要文件扩展名。模板文件必须放在 `_layouts` 目录下。 |
| `permalink` | 如果你需要让你发布的博客的 URL 地址不同于默认值 `/year/month/day/title.html`，那你就设置这个变量，然后变量值就会作为最终的 URL 地址。 |
| `published` | 如果你不想在站点生成后展示某篇特定的博文，那么就设置（该博文的）该变量为 false。 |

## 自定义变量[Permalink](https://darkchoco10099.github.io/2022-04-27-YAML_Front/#自定义变量)

在头信息中没有预先定义的任何变量都会在数据转换中通过 Liquid 模板被调用。例如，如果你设置一个 title 变量，然后你就可以在你的模板中使用这个 title 变量来设置页面的标题（title）：

```html
<!DOCTYPE HTML>
<html>
  <head>
    <title>{{ page.title }}</title>
  </head>
  <body>
    ...
```

## 在文章中预定义的变量[Permalink](https://darkchoco10099.github.io/2022-04-27-YAML_Front/#在文章中预定义的变量)

在文章中可以使用这些在头信息变量列表中未包含的变量。

| 变量名称               | 描述                                                         |
| ---------------------- | ------------------------------------------------------------ |
| `date`                 | 这里的日期会覆盖文章名字中的日期。这样就可以用来保障文章排序的正确。日期的具体格式为`YYYY-MM-DD HH:MM:SS +/-TTTT`；时，分，秒和时区都是可选的。 |
| `category``categories` | 除过将博客文章放在某个文件夹下面外，你还可以指定博客的一个或者多个分类属性。这样当你的站点生成后，这些文章就可以根据这些分类来阅读。`categories` 可以通过 [YAML list](http://en.wikipedia.org/wiki/YAML#Lists)，或者以逗号隔开的字符串指定。 |
| `tags`                 | 类似分类 `categories`，一篇文章也可以给它增加一个或者多个标签。同样，`tags` 可以通过 YAML 列表或者以逗号隔开的字符串指定。 |

- 原文链接：[头信息 - Jekyll • 简单静态博客网站生成器 (jekyllcn.com)](http://jekyllcn.com/docs/frontmatter/)

## 相关yaml配置例子


~~~yaml
# 模板文件
layout: post
# 文章大标题
title: Flake it till you make it
# 文章副标题
subtitle: Excerpt from Soulshaping by Jeff Brown
# 点击进入后文章标题的大图片（横置为佳）
cover-img: /assets/img/path.jpg
# 预览位置的小共享图片
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
# 标签，建议系统化，便于后期当目录查看
tags: [books, test]


layout: post
title: Sample blog post
subtitle: Each post also has a subtitle
# github的repo连接，从用户名开始
gh-repo: daattali/beautiful-jekyll
# github相关repo的相关量统计并显示
gh-badge: [star, fork, follow]
tags: [test]
comments: true
~~~

