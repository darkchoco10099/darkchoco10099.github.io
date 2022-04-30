---
layout: post
title: Django连接Mysql报错
subtitle:  显示没有安装数据库服务
tags: [python, Django, Errors, Mysql]
---

python3 中django连接mysql使用的包是pymysql, 所以第一步先安装 pymysql
pip install pymysql, 安装了并不代表就可以了， 还需要在项目的__init__.py

~~~
myblog/
├── apps
├── Dockerfile
├── manage.py
├── myblog
│   ├── __init__.py   # 此处添加代码
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── statics
└── templates
~~~



~~~python
import pymysql
pymysql.install_as_MySQLdb()
~~~



原文链接：https://blog.csdn.net/weixin_43886133/article/details/102937338