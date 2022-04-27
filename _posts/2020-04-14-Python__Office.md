---
layout: post
title: python办公自动化
subtitle: python + office
tags: [python, office]
---



# Python__Office

## 一、输出目录下所有文件及文件夹

* Python 标准库

* 和操作系统有关的操作

* 有些指令Windows、Mac、Linux通用

  * 详情见：https://docs.python.org/zh-cn/3/library/os.html

* 获取Python程序运行路径

  * **os.getcwd()**

  * ```python
    import os
    
    print(os.getcwd())
    # 输出当前程序的子目录
    ```
  
* 关于路径中的斜杠（/）和反斜杠（\）

  * Windows中采用反斜杠（\）作为分隔符
  * Mac和Linux中才会用斜杠（/）作为分隔符
  * 因为反斜杠再Python中用于转义，所以变为双反斜杠（\ \）

* 让Python自动处理路径连接

  * **os.path.join()**

  * ```python
    import os
    
    print(os.path.join('MyProjects','AI'))
    # windows:'Myprojects\\AI'
    # Mac、Linux:'Myprojects/AI'
    ```

* 相对路径

  * 如果程序运行在E:\pythonPractice\文件夹下
  * 那么这个文件夹中的文件的相对路径可以表示为./practice

* 列出当前程序文件夹下的所有文件和文件夹

  * **os.listdir(指定的相对路径或者绝对路径)**

  * ```python
    import os 
    
    for item in os.listdir():
        print(item)
    ```

* 循环判断是不是文件夹

  * **os.path.isdir(要判断的路径)**

  * ```python
    import os 
    
    files = os.listdir()
    for file in files:
        print(file,os.path.isdir(file))
    # os.path.isdir(file) = TURE  那么就是文件夹
    # os.path.isdir(file) = FALSE 那么就是文件
    ```

  * 更推荐的方法

  * **os.scandir(指定的相对路径或者绝对路径)**

  * ```python 
    import os 
    
    for for file in os.scandir():
        print(file.name,file.path,file.is_dir())
    ```

  * **生成迭代器**

## 二、遍历搜索文件及查询文件信息

* 把文件夹内部所有层级中的所有文件找出来

  * **os.walk(绝对路径或指定路径)**

  * ```python
    import os 
    
    for dirpath,dirnames,files in os.walk('./'):
        print(f'发现文件夹:{dirpath}')
        print(files)
    # dirpath是文件夹路径
    # dirnames是dirpath这个文件夹下的子文件夹列表
    # files是dirpath这个文件夹里的文件列表
    ```

* 利用字符串内置的方法搜索、匹配文件

  * **.startswith() and .endwith()**

  * ```python
    print('abc.txt'.startswith('ab'))
    print('abc.txt'.endwith('.txt'))
    ```

  * 字符串A.statrswith(字符串B)：字符串A是否以字符串B开头

  * 字符串A.endwith(字符串B)：字符串A是否以字符串B结尾

* 利用glob模块的方法搜索、匹配文件

  * **glob.glob()**

  * ```python
    import glob
    
    print(glob.glob('*.py'))
    # *表示任意字符
    ```

  * | 模式   | 意义                    |
      | ------ | ----------------------- |
      | *      | 匹配所有                |
      | ？     | 匹配任何单个字符        |
      | [seq]  | 匹配seq中的任何字符     |
      | [!seq] | 匹配任何不在seq中的字符 |

  * 把深层的文件找出来
  
  * ```python
      print(glob.glob('**/*.txt',recursive = True))
      
      # **表示任意层文件或文件夹
      # recursive = True会不断进入文件夹内
      ```
  
* 利用fnmatch模块匹配文件名

  * ```python
    import fnmatch
    
    print(fnmatch.fnmatch('lesson1.py','le*1.py'))
    print(fnamtch.fnmatch('lesson1.py','le*[0-9].py'))
    #前面的文件名是否符合后面的规则，返回TRUE或FALSE
    ```

* 查询文件信息

  * **os.scandir()返回的文件都可以查询信息**

  * ```python
    import os
    
    for file in os.scandir():
        print(file.stat())
    ```

  * | name               | meaning                                      |
      | ------------------ | -------------------------------------------- |
      | st_size            | 文件的体积大小（单位：bytes）,除以1024就是kb |
      | st_atime（access） | 文件最近访问的时间                           |
      | st_mtime（modify） | 文件最近修改的时间                           |
      | st_ctime（create） | Windows下表示的创建时间                      |
      | st_birthtime       | Mac、Linux下的创建时间                       |
      |                    |                                              |

* Unix时间戳

  * 前面的时间是一个长的字符串,这种时间叫做时间戳

  * 可以利用Python转换为正常的日期时间

  * ```python
    import time
    
    print(time.ctime(srting_num))
    ```

  * **datetime模块**

  * ```python
    import datetime
    
    that_time = datetime.datetime.fromtimestamp(srting_num)
    print(that_time)
    print(that_time.hour,that_time.minute,that_time.second)
    ```

  * datetime模块转换时间

  * ```python
    for file in so.scandir():
        filr_mtime = file.stat().st_mtime
        print(datatime.datetime.fromtimestamp(file_mtime))
    ```

  * 单独查询制定文件

  * **os.stat(指定文件路径)**

  * ```python
    print(os.stat('lesson.py'))
    ```

  * 

