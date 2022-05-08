---
layout: post
title: Django的admin页面没有样式
tags: [python, Error, Django]
---

```python
# setting.py
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')

python manage.py collectstatic

```

