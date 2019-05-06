修改models.py文件

```python
from django.db import models


class UserInfo(models.Model):
    username = models.CharField(max_length=64)
    # 创建username字段，数据类型为charfield类型，类似于char类型
    gender = models.CharField(max_length=64)
    email = models.CharField(max_length=64)

```

#### 创建字段

字段即类里面的属性（变量）

attr = CharField(max_length=64)

#### 生成数据表

命令行中进入**manage.py同级目录**

执行**python manage.py makemigrations add名**（可选）

再执行**python manage.py migrate**

#### 查看

Django会自动在**app/migrations/**目录下生成移植文件

执行**python manage.py sqlmigrate 应用名 文件id** 查看sql语句

**默认sqlite3**的数据库在项目根目录下**db.sqlite3**

#### 页面呈现数据

后台步骤

views.py中import models

article = models.Article.objects.get(pk=1)

render(request,*page*,{'article': article})

前端步骤

模板可直接使用对象以及对象的“.”操作

**{{ article.title }}**

清空数据库

**python manage.py flush**