---
layout: post
title: python爬虫
subtitle: python爬虫基础知识
tags: [python, 爬虫, crawler]
---



# Python_Crawler

## Day 1__get传参

`01_url_open.py`

`02_get_params.py`

***

   > ### 1.python爬取类型：str、bytes
   >
   > > 如果爬取回来的是bytes类型：但是写入的时候需要字符串(str) -->  decode("utf-8")
   > >
   > > 如果爬取回来的是str类型：写入的时候需要bytes类型 -->encode("utf-8")
   >
   > ### 2.汉字报错
   >
   > > python为解释性语言，解析器只支持 ascii，如果出现汉字需要转义
   > > ```python
   > > import urllib.parse
   > > import string
   > > 
   > > encode = urllib.parse.quote(url_final,safe=string.printable)
   > > ```
   >
   > ### 3.urllib.request 用来打开url
   >
   > > ```python
   > > import urllib.request
   > > 
   > > response = urllib.request.urlopen(url)
   > > # url需要没有中文，或者经过上一步转义之后的url_new
   > > ```
   >
   > ### 4.用之前的响应.read().decode()获取数据
   >
   > > ```python
   > > response = urllib.request.urlopen(url)
   > > data = response.read().decode("utf-8")
   > > #decode()内默认是utf-8，所以也可以是 response.read().decode()
   > > ```
   >
   > ### 5.保存到本地
   >
   > > ```python
   > > with open("baidu.html","w",encoding = "utf-8") as f:
   > > 	f.write(data) 
   > > #with open("名称.html","w表示写入",encoding = "utf-8"表示编码为utf-8)
   > > ```
   >
   > ### 6.问题汇总
   >
   > 因为百度有保护机制，所有https需要变为http才能正常爬取
   >
   > ***
   >
   > ### 代码汇总：
   >
   > ```python
   > import urllib.request
   > import urllib.parse
   > import string
   > 
   > def get_method_params():
   >     url = "http://www.baidu.com/s?wd="
   >     #拼接字符串
   >     name = "济南"
   >     url_final = url + name
   >     #python为解释性语言，解析器只支持 ascii，如果出现汉字需要转义
   >     url_newfinal = urllib.parse.quote(url_final,safe=string.printable)
   >     print(url_final)
   >     print(url_newfinal)
   >     response = urllib.request.urlopen(url_newfinal)
   >     print(response)
   >     data = response.read().decode("utf-8")
   >     print(data)
   >     
   >     #将爬取的网页数据写入并生成同文件夹下的test.html
   >     with open("test.html","w",encoding="utf-8")as f:
   >         f.write(data)
   > 
   > get_method_params()
   > ```
   >
   > ### carwler概述：
   >
   > > 1.http:(1)当⽤用户在地址输⼊入了了⽹网址 发送⽹网络请求的过程是什什么
   > > (2)http的请求⽅方式
   > > get请求
   > > (1)⽐比较便便捷
   > > 缺点:不不安全:明⽂文
   > > 参数的⻓长度有限制
   > > post请求
   > > (1)⽐比较安全
   > > (2)数据整体没有限制
   > > (3)上传⽂文件
   > > put(不不完全的)
   > > delete(删除⼀一些信息)
   > > head(请求头)
   > > 发送⽹网络请求(需要带⼀一定的数据给服务器器不不带数据也可以)
   > > 请求头⾥里里⾯面requestheader
   > > 返回数据:response
   > > (1)Accept:⽂文本的格式
   > > (2)Accept-Encoding:编码格式
   > > (3)Connection:⻓长链接 短链接
   > > (4)Cookie:验证⽤用的
   > > (5)Host:域名
   > > (6)Referer:标志从哪个⻚页⾯面跳转过来的
   > > (7)User-Agent:浏览器器和⽤用户的信息
   > > 2.爬⾍虫⼊入⻔门:使⽤用代码模拟⽤用户 批量量的发送⽹网络请求 批量量的获取数据
   > > (1)爬⾍虫的价值:
   > > 1.买卖数据(⾼高端的领域价格特别贵)
   > > 2.数据分析:出分析报告
   > > 3.流量量
   > > 4.指数阿⾥里里指数,百度指数
   > > (3)合法性:灰⾊色产业
   > > 政府没有法律律规定爬⾍虫是违法的,也没有法律律规定爬⾍虫是合法的
   > > 公司概念:公司让你爬数据库(窃取商业机密)责任在公司
   > > (4)爬⾍虫可以爬取所有东⻄西?(不不是)爬⾍虫只能爬取⽤用户能访问到的数据
   > > 爱奇艺的视频(vip⾮非vip)
   > > 1.普通⽤用户 只能看⾮非vip 爬取⾮非vip的的视频
   > > 2.vip 爬取vip的视频
   > > 3.普通⽤用户想要爬取vip视频(⿊黑客)
   > > 爬⾍虫的分类:(1)通⽤用爬⾍虫
   > > 1.使⽤用搜索引擎:百度 ⾕谷歌 360 雅⻁虎 搜狗
   > > 优势:开放性 速度快
   > > 劣势:⽬目标不不明确
   > > 返回内容:基本上%90是⽤用户不不需要的
   > > 不不清楚⽤用户的需求在哪⾥里里
   > > (2)聚焦爬⾍虫(学习)
   > > 1.⽬目标明确
   > > 2.对⽤用户的需求⾮非常精准
   > > 3.返回的内容很固定
   > > 增量量式:翻⻚页:从第⼀一⻚页请求到最后⼀一⻚页
   > > Deep 深度爬⾍虫:静态数据:html css
   > > 动态数据:js代码,加密的js
   > > robots:是否允许其他爬⾍虫(通⽤用爬⾍虫)爬取某些内容
   > > 聚焦爬⾍虫不不遵守robots
   > > 爬⾍虫和反扒做⽃斗争:资源对等 胜利利的永远是爬⾍虫
   > > 爬⾍虫的⼯工作原理理:
   > > 1.缺⼈人你抓取⽬目标的url是哪⼀一个(找)
   > > 2.使⽤用python代码发送请求获取数据(java Go)
   > > 3.解析获取到的数据(精确数据)
   > > (1)找到新的⽬目标(url)回到第⼀一步(⾃自动化)
   > > 4.数据持久化
   > > python3(原⽣生提供的模块):urlib.rquest:
   > > (1)urlopen :
   > > 1.返回response对象
   > > 2.response.read()
   > > 3.bytes.decode("utf-8")
   > > (2)get:传参
   > > 1.汉字报错 :解释器器ascii没有汉字,url汉字转码
   > > (3)post
   > > (4)handle处理理器器的⾃自定义
   > > (5)urlError
   > > python(原⽣生提供的):urlib2
   > > 接下来将的知识点:
   > > 5.request(第三⽅方)
   > > 6.数据解析:xpath bs4
   > > 7.数据存储

***

***

***

## Day 2

`03_get_params_2.py`

`04_request_header.py`

`05_random_user_agent.py`

***

***网站本身有自己的反爬虫机制，如果多次用一个浏览器，即一个user_agent多次频繁的访问同一个网站会出现错误，所以要用不同的头中的不同的user_agent来对网站造成假象***

***

> ### 1.字典传参
> > ```python
> > import urllib.request
> > import urllib.parse
> > 
> > params = {
> >     "wd" : "中文",
> >     "value" : "san",
> >     "key" : "zhang"
> >     #创建字典
> > }
> >     #将字典中的字符进行转义，用到urllib.parse.urlencode
> >     str_params = urllib.parse.urlencode(params)
> > ```
> ### 2.请求头
>
> >#### (1)获取请求头
> >
> >* 通过字典的方式来添加请求头
> >> ```python
> >>#添加请求头的信息
> >>header = {
> >>       #浏览器的版本
> >>       "user-agent" : "Mozilla/5.0 (iPad; CPU OS 11_0 like Mac OS > >X) AppleWebKit/604.1.34 (KHTML, like Gecko) Version/11.0 Mobile/15A5341f Safari/604.1"
> >>}
> >>```
> >* 通过动态的方式来添加请求头
> >>```python
> >>#通过动态的方式来添加请求头
> >>requset.add_header("user-agent","Mozilla/5.0 (iPad; CPU OS 11_0 like Mac OS X) AppleWebKit/604.1.34 (KHTML, like Gecko) Version/11.0 Mobile/15A5341f Safari/604.1")
> >>```
> >#### (2)打印请求头
> >
> >* 在`urllib.request.Request()`中添加字典形式的请求头
> >>
> >>```python
> >>#创建请求对象
> >>requset = urllib.request.Request(url,headers=header)
> >>#获取打印请求头的信息
> >> requset_headers = requset.headers
> >> print(requset_headers)
> >>#获取完整url 
> >>final_url = requset.get_full_url()
> >>
> >>#Request 方法的原函数
> >>"""class Request:
> >>
> >>def __init__(self, url, data=None, headers={},
> >>            origin_req_host=None, unverifiable=False,
> >>            method=None):"""
> >>
> >>```
> >>
> >>
> >* 在request.get_header中直接调用请求头中字典的内容
> >>
> >>  其中，引号内的内容无论原来字典怎么写的，在这里首字母大写其他字母小写
> >>
> >>  ```python
> >>   #获取请求头的信息
> >>  #"User-agent"首字母大写，其他字母小写，不管原来字典什么样
> >>  requset_headers = requset.get_header("User-agent")
> >>  print(requset_headers)
> >>  ```
> >
>
> ### 3.用户标识
>
> **`user-agent`**
>
> ***网站本身有自己的反爬虫机制，如果多次用一个浏览器，即一个user_agent多次频繁的访问同一个网站会出现错误，所以要用不同的头中的不同的user_agent来对网站造成假象,模拟真实浏览器来访问***
>
> >* (1)模拟真实的浏览器器发送请求:(1)百度批量量搜索(2)检查元素(百度搜索`user-agent`⼤大全)
> >* (2)`request.add_header`(动态添加head数据)
> >* (3)响应头` response.header`
> >* (4)创建`request:urlib.request.Request(url)`
> ### 4.IP代理
> >* (1)免费的IP:时效性差,错误率⾼
> >
> >* (2)付费的IP:贵花钱,也有失效不能⽤的
> >
>
>  **IP分类**
>
> >   * (1)透明:对方知道我们真实的ip
> >   * (2)匿名:对方不知道我们真实的ip,知道了你使⽤用了代理
> >   * (3)高匿:对方不知道我们真是的IP.也不知道我们使⽤用了代理
>
> ### 5.自定义`urlopen`来具有添加代理的功能
>
> > 系统的`urlopen`并没有添加代理的功能素以需要自定义这个功能
> >
> > ssl（安全套接层） 第三方CA数字证书







 