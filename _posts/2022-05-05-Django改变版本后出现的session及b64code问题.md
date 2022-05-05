---
layout: post
title: Django改变版本后出现的session及b64code问题
tags: [python, Django, Errors]
---

## Django改变版本后出现的session及b64code问题

报错如下：
File “django/contrib/sessions/backends/base.py”, line 110, in decode
encoded_data = base64.b64decode(session_data.encode(‘ascii’))
File “python3.6/base64.py”, line 87, in b64decode
return binascii.a2b_base64(s)
binascii.Error: Incorrect padding
解决：
由于django版本由3.1.4变为2.2，此错误与迁移无关，但与会话和服务器的更改有关
运行下列代码 或者 直接删除数据库中的
django_session表中数据

```python
from django.contrib.sessions.models import Session
Session.objects.all().delete()
```

