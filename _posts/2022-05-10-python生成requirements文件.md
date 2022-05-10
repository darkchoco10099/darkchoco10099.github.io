---
layout: post
title: python生成requirements.txt文件的两种操作
tags: [python, 持久积累]
---

- 使用```pip freeze```生成

  ~~~powershell
  pip freeze > D:\pycharm\requirements.txt
  ~~~

  特点是全部依赖包都会生成，比较适合虚拟环境

- 使用` pipreqs`

  ~~~powershell
  pip install pipreqs
  ~~~

  ~~~powershell
  pipreqs 当前Python项目的根目录
  ~~~

  特点是只会生成当前项目的依赖，但是不咋好用，生成包不全