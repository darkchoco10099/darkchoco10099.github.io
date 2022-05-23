---
layout: post
title: conda新增环境报HTTP error
tags: [python, anaconda, Errors]
---



~~~
# 错误信息
CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://repo.continuum.io/pk gs/r/win-64/repodata.json.bz2>
~~~



- Solution 1

![image-20220523222540882](https://cdn.jsdelivr.net/gh/darkchoco10099/img/image-20220523222540882.png)

- Solution 2

  ![image-20220523223023881](https://cdn.jsdelivr.net/gh/darkchoco10099/img/image-20220523223023881.png)

- Solution 3

  ![image-20220523223100585](https://cdn.jsdelivr.net/gh/darkchoco10099/img/image-20220523223100585.png)

- Solution 4

**关闭代理！！！！！！！！！！**

参考链接：[python - CondaHTTPError: HTTP 000 CONNECTION FAILED for url - Stack Overflow](https://stackoverflow.com/questions/50305725/condahttperror-http-000-connection-failed-for-url-https-repo-continuum-io-pk)