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
conn = pymysql.connect(host='127.0.0.1', port=3306, user='root', passwd='root', charset='utf8', db='database_name')
cursor = conn.cursor(cursor=pymysql.cursors.DictCursor)

# 2、发送指令
cursor.execute("insert into admin(username,password,mobile) values('zhangsan', '123', '15500009999')")
conn.commit()

# 3、关闭
cursor.close()
conn.close()
~~~

- Django开发操作数据库

![](https://cdn.jsdelivr.net/gh/darkchoco10099/img/image-20220501151558195.png)

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
  
  # 新建表
  class UserInfo(models.Model):
      name = models.CharField(max_length=32)
      paw = models.CharField(max_length=32)
      age = models.IntergerField(default=20)
      
  """
  orm会自动转化执行语句：
  create table appname(相应app名称)_UserInfo(
  	id bigint quto_increment primary key,
  	name varchar(32),
  	password varchar(32)
  	age int
  );
  """

  # 新建数据
  UserInfo.objects.create(name='zhangsan',paw='123',age=23)
  
  # 删除数据
UserInfo.objects.filter(id=3).delete()
  UserInfo.objects.all().delete()

  # 获取数据
  # data_list = [x,x,x,...]
  data_list = UserInfo.objects.all()
  # .first()得到一个对象，取的是第一条数据
  row_obj = UserInfo.objects.filter(id=2).first()
  for obj in data_list：
  	print(obj.id, obj.name, obj.paw, obj.age)
      
  # 更新数据
  UserInfo.objects.all().update(age=23)
  UserInfo.objects.filter(id=45).update(age=56)
  ```
  
  - ```python
    makemigrations
    migrate
    ```
  
  - app需要提前注册到settings里面
  
  





# 建立一个[MODEL](https://so.csdn.net/so/search?q=MODEL&spm=1001.2101.3001.7020)

当然，为了方便讲解，我们还是建立一个简单的Model：

```python
from django.db import models

class BookInfo(models.Model):
    title = models.CharField(max_length=20, verbose_name='名称')
    number = models.IntegerField(default=0, verbose_name='数量')
    comment = models.IntegerField(default=0, verbose_name='评论数量')
    is_delete = models.BooleanField(default=False, verbose_name='逻辑删除')

    class Meta:
        db_table = 'books'
        verbose_name = '图书'   # 在管理员admin站点中显示的名称

    def __str__(self):
        return self.btitle

class StudentInfo(models.Model):
	"""
	看是男是女
	"""
    GENDER_CHOICES = (
        (0, 'female'),
        (1, 'male')
    )
    class Meta:
        db_table = 'students'
        verbose_name = '学生'
    name = models.CharField(max_length=20, verbose_name='名称')
    #  default 为缺省值 这点很重要哦！！！
    gender = models.SmallIntegerField(choices=GENDER_CHOICES, default=0, verbose_name='性别')
    info = models.CharField(max_length=200, null=True, verbose_name='信息')
    book = models.ForeignKey(BookInfo, on_delete=models.CASCADE, verbose_name='图书名称') # 外键,不能省略
    is_delete = models.BooleanField(default=False, verbose_name='删除')

    def __str__(self):
        return self.hname

```

# 数据库操作（正题）

## 给数据库中模型增加元素

### 使用save方法

```python
book=BookInfo(title='高等数学',number='10000',comment='400')
book.save()

```

上面这个等价于：

```python
book=BookInfo()
book.title = 'xxx'
book.number = 'xxx'
book.comment = 'xxx'
book.save()

```

### 使用create方法

```python
StudentInfo.objects.create(name='豪哥哥'gender='1',info='小可爱',book=book)

```

### 防止重复创建

🌂：首先尝试获取，不存在就创建，可以防止重复

```python
StudentInfo.objects.get_or_create(name='豪哥哥'gender='1',info='小可爱',book=book)

```

🌂：最后一种方法返回一个元组，(object, True/False)，创建时返回 True, 已经存在时返回 False

## 数据库内容的修改

### 使用update方法

当然`filter`中的查找条件也可以改为其他的后面会讲解

```python
StudentInfo.objects.filter(info='小可爱').update(info='大可爱')

```

### 使用get方法配合save方法

🌂：关于`__exact`后面也会讲解的

```python
# 两种方式
stu = StudentInfo.objects.get(gender__exact = 1)   # 可以且仅可以返回一条数据。 没有数据或返回多条数据都会抛异常。
stu = StudentInfo.objects.get(gender= 1)   # 简写形式 __exact可以省略。返回模型对象
stu.name = "小帅哥"
stu.save()

```

## 数据库内容的查询

### get函数（上面提了这里不多讲）

(知道get返回一条数据就ok！)

### all函数 (查询所有)

```python
students = StudentInfo.objects.all()   # 查询所有,返回QuerySet查询集(可以遍历)

```

迭代用法如下所示：

```python
stu = StudentInfo.objects.all()
for i in stu:
    print(i.name)

```

🌂：多说一点，如果想要知道数据库中有多少条数据，可以使用`count`方法

```python
StudentInfo.objects.count()
结果简单来说就是有多少行，很容易理解对吧

```

### filter函数 (条件查询)

`属性名称__比较运算符=你要修改的内容`
注意了！！！敲重点！！！
属性名称和比较运算符间使用`两个`下划线，记住是`两个`

#### exact的使用

前面已经提到过，搬运工哈哈哈

```python
# 两种方式
stu = StudentInfo.objects.get(gender__exact = 1)   # 可以且仅可以返回一条数据。 没有数据或返回多条数据都会抛异常。
stu = StudentInfo.objects.get(gender= 1)   # 简写形式 __exact可以省略。返回模型对象

```

#### contains、startswith、endswith（模糊查询）

从单词字面意思可知：
`contains`:查询包含"某个值"
`statwith`：以什么开头
`endswith`:以什么结尾
这里不给例子了

#### 空值查询

🌂：查询学生名不为空的学生名

```python
StudentInfo.objects.filter(title__isnull=False)

```

返回`QuerySet`对象：

```python
<QuerySet [<BookInfo: 豪哥哥>, <BookInfo: 小哥哥>>

```

#### 比较查询

`gt` :大于 (greater then)
`gte`:大于等于 (greater then equal)
`lt` :小于 (less then)
`lte` :小于等于 (less then equal)
随便整一个例子：

```python
BooktInfo.objects.filter(number__gte=200)

```

#### exclude函数 (filter函数取反)

查询number不为300的所有图书。

```python
books = BookInfo.objects.exclude(number = 300)
 # 与filter函数作用相反
 #返回QuerySet查询集(可以遍历)

```

#### order\_by函数 (排序)

```python
books = BookInfo.objects.all().order_by('-number')   # 'id'表示升序； '-number'表示降序。
books = BookInfo.objects.order_by('-number')   #  其实.all()可以省略。 默认查询所有。最好还是加上吧！
# 对查询结果进行排序
# 返回QuerySet

```

暂时到这里吧，觉得基础比较实用的部分！



