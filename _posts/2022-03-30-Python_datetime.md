---
layout: post
title: pyhton datetime
subtitle: 介绍了python中datetime模块的基本使用
tags: [python, datetime]
---



python中的datetime模块提供了操作日期和时间功能,本文为大家讲解了datetime模块的使用方法及与其相关的日期比较，计算实例

python中的datetime模块提供了操作日期和时间功能,该模块提供了五种核心对象:datetime时间日期类型,date日期类型,time时间类型,tzinfo时区类型,timedelta时间差类型，今天为大家介绍一下datetime模块的具体使用方法与python日期时间计算与比较的相关实例

### 一、Python中日期时间模块datetime介绍

#### （一）、datetime模块中包含如下类：

| 类名          | 功能说明                                                   |
| :------------ | :--------------------------------------------------------- |
| date          | 日期对象,常用的属性有year, month, day                      |
| time          | 时间对象                                                   |
| datetime      | 日期时间对象,常用的属性有hour, minute, second, microsecond |
| datetime_CAPI | 日期时间对象C语言接口                                      |
| timedelta     | 时间间隔，即两个时间点之间的长度                           |
| tzinfo        | 时区信息对象                                               |

#### （二）、datetime模块中包含的常量

| 常量    | 功能说明             | 用法             | 返回值 |
| :------ | :------------------- | :--------------- | :----- |
| MAXYEAR | 返回能表示的最大年份 | datetime.MAXYEAR | 9999   |
| MINYEAR | 返回能表示的最小年份 | datetime.MINYEAR | 1      |

### 二、date类

#### （一）、date对象构成

1、date对象由`year`年份、`month`月份及`day`日期三部分构成：

```
date``（year，month，day)
```

2、 通过`year`, `month`, `day`三个数据描述符可以进行访问：

```
>>> a = datetime.``date``.today()``>>> a``datetime.``date``(2017, 3, 22)``>>> a.year``2017``>>> a.month``3``>>> a.day``22
```

3、当然，你也可以用`__getattribute__(...)`方法获得上述值：

```
>>> a.__getattribute__(``'year'``)``2017``>>> a.__getattribute__(``'month'``)``3``>>> a.__getattribute__(``'day'``)``22
```

#### （二）、date对象中包含的方法与属性

##### 1、用于日期比较大小的方法

| 方法名    | 方法说明       | 用法        |
| :-------- | :------------- | :---------- |
| __eq__(…) | 等于(x==y)     | x.__eq__(y) |
| __ge__(…) | 大于等于(x>=y) | x.__ge__(y) |
| __gt__(…) | 大于(x>y)      | x.__gt__(y) |
| __le__(…) | 小于等于(x<=y) | x.__le__(y) |
| __lt__(…) | 小于(x         | x.__lt__(y) |
| __ne__(…) | 不等于(x!=y)   | x.__ne__(y) |

以上方法的返回值为True\False
示例如下：

```
>>> a=datetime.``date``(2017,3,1)``>>> b=datetime.``date``(2017,3,15)``>>> a.__eq__(b)``False``>>> a.__ge__(b)``False``>>> a.__gt__(b)``False``>>> a.__le__(b)``True``>>> a.__lt__(b)``True``>>> a.__ne__(b)``True
```

##### 2、获得二个日期相差多少天

使用`__sub__(...)`和`__rsub__(...)`方法，其实二个方法差不太多，一个是正向操作，一个是反向操作：

| 方法名      | 方法说明 | 用法          |
| :---------- | :------- | :------------ |
| __sub__(…)  | x - y    | x.__sub__(y)  |
| __rsub__(…) | y - x    | x.__rsub__(y) |

示例如下:

```
>>> a``datetime.``date``(2017, 3, 22)``>>> b``datetime.``date``(2017, 3, 15)``>>> a.__sub__(b)``datetime.timedelta(7)``>>> a.__rsub__(b)``datetime.timedelta(-7)
```

计算结果的返回值类型为`datetime.timedelta`, 如果获得整数类型的结果则按下面的方法操作：

```
>>> a.__sub__(b).days``7``>>> a.__rsub__(b).days``-7
```

##### 3、ISO标准化日期

如果想要让所使用的日期符合ISO标准，那么使用如下三个方法:
1).** `isocalendar(...)`**:返回一个包含三个值的元组，三个值依次为：`year`年份，`week number`周数，`weekday`星期数（周一为1…周日为7)：
示例如下

```
>>> a = datetime.``date``(2017,3,22)``>>> a.isocalendar()``(2017, 12, 3)``>>> a.isocalendar()[0]``2017``>>> a.isocalendar()[1]``12``>>> a.isocalendar()[2]``3
```

2). `isoformat(...)`: 返回符合ISO 8601标准 (`YYYY-MM-DD`) 的日期字符串；
示例如下

```
>>> a = datetime.``date``(2017,3,22)``>>> a.isoformat()``'2017-03-22'
```

3). `isoweekday(...)`: 返回符合ISO标准的指定日期所在的星期数（周一为1…周日为7)
示例如下：

```
>>> a = datetime.``date``(2017,3,22)``>>> a.isoweekday()``3
```

4).与`isoweekday(...)`相似的还有一个`weekday(...)`方法，只不过是`weekday(...)`方法返回的周一为 0, 周日为 6
示例如下：

```
>>> a = datetime.``date``(2017,3,22)``>>> a.weekday()``2
```

##### 4、其他方法与属性

1). `timetuple(...)`:该方法为了兼容`time.localtime(...)`返回一个类型为`time.struct_time`的数组，但有关时间的部分元素值为0：

```
>>> a = datetime.``date``(2017,3,22)``>>> a.timetuple()``time``.struct_time(tm_year=2017, tm_mon=3, tm_mday=22, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=2, tm_yday=81, tm_isdst=-1)``>>> a.timetuple().tm_year``2017``>>> a.timetuple().tm_mon``3``>>> a.timetuple().tm_mday``22
```

2).`toordinal(...)`： 返回公元公历开始到现在的天数。公元1年1月1日为1

```
>>> a = datetime.``date``(2017,3,22)``>>> a.toordinal()``736410
```

3). `replace(...)`：返回一个替换指定日期字段的新date对象。参数3个可选参数，分别为year,month,day。注意替换是产生新对象，不影响原date对象。

```
>>> a = datetime.``date``(2017,3,22)``>>> b = a.replace(2017,2,28)``>>> a``datetime.``date``(2017, 3, 22)``>>> b``datetime.``date``(2017, 2, 28)
```

4).`resolution`：date对象表示日期的最小单位。这里是天。

```
>>> datetime.``date``.resolution``datetime.timedelta(1)
```

5).`fromordinal(...)`：将Gregorian日历时间转换为date对象；Gregorian Calendar ：一种日历表示方法，类似于我国的农历，西方国家使用比较多。

```
>>> a = datetime.``date``(2017,3,22)``>>> b = a.toordinal()``>>> datetime.``date``.fromordinal(b)``datetime.``date``(2017, 3, 22)
```

6).`fromtimestamp(...)`：根据给定的时间戮，返回一个date对象

```
>>> ``time``.``time``()``1490165087.2242179``>>> datetime.``date``.fromtimestamp(``time``.``time``())``datetime.``date``(2017, 3, 22)
```

7).`today(...)`：返回当前日期

```
>>> datetime.``date``.today()``datetime.``date``(2017, 3, 22)
```

8).`max`： date类能表示的最大的年、月、日的数值

```
>>> datetime.``date``.max``datetime.``date``(9999, 12, 31)
```

9).`min`： date类能表示的最小的年、月、日的数值

```
>>> datetime.``date``.min``datetime.``date``(1, 1, 1)
```

#### （三）、日期的字符串输出

1、如果你想将日期对象转化为字符串对象的话，可以用到`__format__(...)`方法以指定格式进行日期输出：

```
>>> a = datetime.``date``(2017,3,22)``>>> a.__format__(``'%Y-%m-%d'``)``'2017-03-22'``>>> a.__format__(``'%Y/%m/%d'``)``'2017/03/22'``>>> a.__format__(``'%y/%m/%d'``)``'17/03/22'``>>> a.__format__(``'%D'``)``'03/22/17'
```

与此方法等价的方法为`strftime(...)`

```
>>> a.strftime(``"%Y%m%d"``)``'20170322'
```

关于格式化字符串的相关内容，请查阅本文最后的：附录：python中时间日期格式化符号
2、如果只是相简单的获得日期的字符串，则使用`__str__(...)`

```
>>> a.__str__()``'2017-03-22'
```

3、如果想要获得ctime样式的格式请使用`ctime(...)`:

```
>>> a.ctime()``'Wed Mar 22 00:00:00 2017'
```

### 三、time类

#### (一)、time类的数据构成

`time`类由`hour`小时、`minute`分钟、`second`秒、`microsecond`毫秒和`tzinfo`五部分组成

```
time``([hour[, minute[, second[, microsecond[, tzinfo]]]]])
```

相应的，time类中就有上述五个变量来存储应该的值：

```
>>> a = datetime.``time``(12,20,59,899)``>>> a``datetime.``time``(12, 20, 59, 899)``>>> a.hour``12``>>> a.minute``20``>>> a.second``59``>>> a.microsecond``899``>>> a.tzinfo
```

与`date`类一样，`time`类也包含`__getattribute__(...)`方法可以读取相关属性：

```
>>> a.__getattribute__(``'hour'``)``12``>>> a.__getattribute__(``'minute'``)``20``>>> a.__getattribute__(``'second'``)``59
```

#### （二）、time类中的方法和属性

##### 1、python比较时间大小

相关方法包括：`__eq__(...)`, `__ge__(...)`, `__gt__(...)`, `__le__(...)`, `__lt__(...)`， `__ne__(...)`
这里的方法与`date`类中定义的方法大同小异，使用方法与一样，这里就不过多介绍了，示例如下：

```
>>> a = datetime.``time``(12,20,59,899)``>>> b = datetime.``time``(11,20,59,889)``>>> a.__eq__(b)``False``>>> a.__ne__(b)``True``>>> a.__ge__(b)``True``>>> a.__gt__(b)``True``>>> a.__le__(b)``False``>>> a.__lt__(b)``False
```

##### 2、`__nonzero__(...)`

判断时间对象是否非零，返回值为True/False:

```
>>> a = datetime.``time``(12,20,59,899)``>>> a.__nonzero__()``True
```

##### 3、其他属性

1）、`max`：最大的时间表示数值：

```
>>> datetime.``time``.max``datetime.``time``(23, 59, 59, 999999)
```

2）、`min`：最小的时间表示数值

```
>>> datetime.``time``.min``datetime.``time``(0, 0)
```

3）、`resolution`：时间间隔单位为分钟

```
>>> datetime.``time``.resolution``datetime.timedelta(0, 0, 1)
```

#### （三）、时间的字符串输出

1、如果你想将时间对象转化为字符串对象的话，可以用到`__format__(...)`方法以指定格式进行时间输出：

```
>>> a = datetime.``time``(12,20,59,899)``>>> a.__format__(``'%H:%M:%S'``)``'12:20:59'
```

与此方法等价的方法为`strftime(...)`

```
>>> a = datetime.``time``(12,20,59,899)``>>> a.strftime(``'%H:%M:%S'``)``'12:20:59'
```

关于格式化字符串的相关内容，请查阅本文最后的：附录：python中时间日期格式化符号

2、ISO标准输出

如果要使输出的时间字符符合ISO标准，请使用`isoformat(...)`:

```
>>> a = datetime.``time``(12,20,59,899)``>>> a.isoformat()``'12:20:59.000899'
```

3、如果只是相简单的获得时间的字符串，则使用`__str__(...)`

```
>>> a = datetime.``time``(12,20,59,899)``>>> a.__str__()``'12:20:59.000899'
```

### 四、datetime类

#### (一)、datetime类的数据构成

`datetime`类其实是可以看做是`date`类和`time`类的合体，其大部分的方法和属性都继承于这二个类，相关的操作方法请参阅，本文上面关于二个类的介绍。其数据构成也是由这二个类所有的属性所组成的。

```
datetime(year, month, day[, hour[, minute[, second[, microsecond[,tzinfo]]]]])
```

#### （二）、专属于datetime的方法和属性

##### 1、 date(…)：返回datetime对象的日期部分：

```
>>> a = datetime.datetime.now()``>>> a``datetime.datetime(2017, 3, 22, 16, 9, 33, 494248)``>>> a.``date``()``datetime.``date``(2017, 3, 22)
```

##### 2、time(…)：返回datetime对象的时间部分：

```
>>> a = datetime.datetime.now()``>>> a``datetime.datetime(2017, 3, 22, 16, 9, 33, 494248)``>>> a.``time``()``datetime.``time``(16, 9, 33, 494248)
```

#### 3、utctimetuple(…)：返回UTC时间元组：

```
>>> a = datetime.datetime.now()``>>> a``datetime.datetime(2017, 3, 22, 16, 9, 33, 494248)``>>> a.utctimetuple()``time``.struct_time(tm_year=2017, tm_mon=3, tm_mday=22, tm_hour=16, tm_min=9, tm_sec=33, tm_wday=2, tm_yday=81, tm_isdst=0)
```

#### 4、combine(…)：将一个date对象和一个time对象合并生成一个datetime对象：

```
>>> a = datetime.datetime.now()``>>> a``datetime.datetime(2017, 3, 22, 16, 9, 33, 494248)``>>>datetime.datetime.combine(a.``date``(),a.``time``())``datetime.datetime(2017, 3, 22, 16, 9, 33, 494248)
```

#### 5、now(…)：返回当前日期时间的datetime对象：

```
>>> a = datetime.datetime.now()``>>> a``datetime.datetime(2017, 3, 22, 16, 9, 33,
```

#### 6、utcnow(…):返回当前日期时间的UTC datetime对象：

```
>>> a = datetime.datetime.utcnow()``>>> a``datetime.datetime(2017, 3, 22, 8, 26, 54, 935242)
```

#### 7、strptime(…)：根据string, format 2个参数，返回一个对应的datetime对象：

```
>>> datetime.datetime.strptime(``'2017-3-22 15:25'``,``'%Y-%m-%d %H:%M'``)``datetime.datetime(2017, 3, 22, 15, 25)
```

#### 8、utcfromtimestamp(…):UTC时间戳的datetime对象，时间戳值为time.time()：

```
>>> datetime.datetime.utcfromtimestamp(``time``.``time``())``datetime.datetime(2017, 3, 22, 8, 29, 7, 654272)
```

### 五、timedelta类

`timedelta`类是用来计算二个`datetime`对象的差值的。

此类中包含如下属性：

1、`days`:天数

2、`microseconds`：微秒数(>=0 并且 <1秒）

3、`seconds`：秒数(>=0 并且 <1天）

### 六、python日期计算实例

#### 1.Python获取当前日期时间：

```
>>> now = datetime.datetime.now()``>>> now``datetime.datetime(2017, 3, 22, 16, 55, 49, 148233)``>>> today = datetime.``date``.today()``>>> today``datetime.``date``(2017, 3, 22)``>>> now.``date``()``datetime.``date``(2017, 3, 22)``>>> now.``time``()``datetime.``time``(16, 55, 49, 148233)
```

#### 2.Python获取上个月第一天和最后一天的日期：

```
>>> today = datetime.``date``.today()``>>> today``datetime.``date``(2017, 3, 22)``>>> mlast_day = datetime.``date``(today.year, today.month, 1) - datetime.timedelta(1)``>>> mlast_day``datetime.``date``(2017, 2, 28)``>>> mfirst_day = datetime.``date``(mlast_day.year, mlast_day.month, 1)``>>> mfirst_day``datetime.``date``(2017, 2, 1)
```

#### 3.Python获取时间差

时间差单位为秒

```
>>> start_time = datetime.datetime.now()``>>> end_time = datetime.datetime.now()``>>> (end_time - start_time).seconds``7
```

差值不只是可以查看相差多少秒，还可以查看天(days), 秒(seconds), 微秒(microseconds).

#### 4.Python计算当前时间向后8个小时的时间

```
>>> d1 = datetime.datetime.now()``>>> d2 = d1 + datetime.timedelta(hours = 8)``>>> d2``datetime.datetime(2017, 3, 23, 1, 10, 37, 182240)
```

可以计算: 天(days), 小时(hours), 分钟(minutes), 秒(seconds), 微秒(microseconds).

#### 5.Python计算上周一和周日的日期

```
today = datetime.``date``.today()``>>> today``datetime.``date``(2017, 3, 23)``>>> today_weekday = today.isoweekday()``>>> last_sunday = today - datetime.timedelta(days=today_weekday)``>>> last_monday = last_sunday - datetime.timedelta(days=6)``>>> last_sunday``datetime.``date``(2017, 3, 19)``>>> last_monday``datetime.``date``(2017, 3, 13)
```

#### 6.Python计算指定日期当月最后一天的日期和本月天数

```
>>> ``date` `= datetime.``date``(2017,12,20)``>>> def eomonth(date_object):``... ``if` `date_object.month == 12:``...  next_month_first_date = datetime.``date``(date_object.year+1,1,1)``... ``else``:``...  next_month_first_date = datetime.``date``(date_object.year, date_object.month+1, 1)``... ``return` `next_month_first_date - datetime.timedelta(1)``...``>>> eomonth(``date``)``datetime.``date``(2017, 12, 31)``>>> eomonth(``date``).day``31
```

#### 7.Python计算指定日期下个月当天的日期

这里要调用上一项中的函数`eomonth(...)`

```
>>> ``date` `= datetime.``date``(2017,12,20)      ``>>> def edate(date_object):       ``... ``if` `date_object.month == 12:    ``...  next_month_date = datetime.``date``(date_object.year+1, 1,date_object.day)``... ``else``:``...  next_month_first_day = datetime.``date``(date_object.year,date_object.month+1,1)``...  ``if` `date_object.day > eomonth(last_month_first_day).day:``...  next_month_date = datetime.``date``(date_object.year,date_object.month+1,eomonth(last_month_first_day).day)``...  ``else``:``...  next_month_date = datetime.``date``(date_object.year, date_object.month+1, date_object.day)``... ``return` `next_month_date``...``>>> edate(``date``)``datetime.``date``(2018, 1, 20)
```

#### 8.Python获得本周一至今天的时间段并获得上周对应同一时间段

```
>>> today = datetime.``date``.today()``>>> this_monday = today - datetime.timedelta(today.isoweekday()-1)``>>> last_monday = this_monday - datetime.timedelta(7)``>>> last_weekday = today -datetime.timedelta(7)``>>> this_monday``datetime.``date``(2017, 3, 20)``>>> today``datetime.``date``(2017, 3, 23)``>>> last_monday``datetime.``date``(2017, 3, 13)``>>> last_weekday``datetime.``date``(2017, 3, 16)
```

### 附录：python中时间日期格式化符号：

| 符号 | 说明                                      |
| :--- | :---------------------------------------- |
| %y   | 两位数的年份表示（00-99）                 |
| %Y   | 四位数的年份表示（000-9999）              |
| %m   | 月份（01-12）                             |
| %d   | 月内中的一天（0-31）                      |
| %H   | 24小时制小时数（0-23）                    |
| %I   | 12小时制小时数（01-12）                   |
| %M   | 分钟数（00=59）                           |
| %S   | 秒（00-59）                               |
| %a   | 本地简化星期名称                          |
| %A   | 本地完整星期名称                          |
| %b   | 本地简化的月份名称                        |
| %B   | 本地完整的月份名称                        |
| %c   | 本地相应的日期表示和时间表示              |
| %j   | 年内的一天（001-366）                     |
| %p   | 本地A.M.或P.M.的等价符                    |
| %U   | 一年中的星期数（00-53）星期天为星期的开始 |
| %w   | 星期（0-6），星期天为星期的开始           |
| %W   | 一年中的星期数（00-53）星期一为星期的开始 |
| %x   | 本地相应的日期表示                        |
| %X   | 本地相应的时间表示                        |
| %Z   | 当前时区的名称                            |
| %%   | %号本身                                   |