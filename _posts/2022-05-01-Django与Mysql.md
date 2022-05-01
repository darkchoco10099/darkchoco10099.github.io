---
layout: post
title: Django与Mysql的连接与开发
subtitle: Django框架与Mysql等数据库的联动，通过pymsql与orm等操作简化操作
tags: [python, 全栈开发, Django, Mysql, orm]
---

通过pymysql可以使python能够轻松地操作数据库内容，而通过django的orm框架则可以更简单的操作数据库。

- Mysql + pymysql

~~~ python
import pymysql

# 1、连接mysql
conn = pymsql.connect(host='127.0.0.1', port=3306, user='root', passwd='root', charset='utf8', db='database_name')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)

# 2、发送指令
cursor.execute("insert into admin(username,password,mobile) values('zhangsan', '123', '15500009999')")
conn.commit()

# 3、关闭
cursor.close()
conn.close()
~~~

- Django开发操作数据库

![image-20220501151558195](2022-05-01-Django与Mysql.assets/image-20220501151558195.png)

- `	pymsql`有一个源码的错误，需要在`__init__`中添加代码，可以安装` mysqlclient`避免

  - 如果用了pymsql，则需要在项目同名目录下的`__init__`中添加：

    ~~~python
    import pymysql
    pymysql.install_as_MySQLdb()
    ~~~

- ORM可以帮我们做两件事：
  - 创建、修改、删除数据库中的表（不用写SQL语句）。【无法创建数据库】
  - 操作表中得数据。（不用写SQL语句）
- settings中增加外界数据库

```pyhton
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'database_name',
        'USER': 'root',
        'PASSWORD': 'root',
        'HOST': '127.0.0.1',
        'POST': 3306,
    }
}
```

- django操作表

  - 在models.py中添加class

  ```python
  from django.db import models
  
  class UserInfo(models.Model):
      name = models.CharField(max_length=32)
      paw = models.CharField(max_length=32)
      age = models.IntergerField()
      
  """
  orm会自动转化执行语句：
  create table appname(相应app名称)_UserInfo(
  	id bigint quto_increment primary key,
  	name varchar(32),
  	password varchar(32)
  	age int
  );
  """
  ```

  - ```python
    makemigrations
    migrate
    ```

  - app需要提前注册到settings里面

  