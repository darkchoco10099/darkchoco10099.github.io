---
layout: post
title: No module named 'mysql'
tags: [python, Django, Errors]
---

ModuleNotFoundError: No module named 'mysql'

### 若 导入MySQL驱动:

 import mysql.connector

### 需要安装MySQL驱动

由于MySQL服务器以独立的进程运行，并通过网络对外服务，所以，需要支持Python的MySQL驱动来连接到MySQL服务器。MySQL官方提供了mysql-connector-python驱动，但是安装的时候需要给pip命令加上参数`--allow-external`：

```undefined
pip install mysql-connector-python mysql-connector-python
```

或者

```
pip install mysql-connector-python --allow-external mysql-connector-python
```

 或者

```undefined
pip install mysql-connector
```