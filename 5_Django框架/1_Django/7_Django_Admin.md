### 什么是Admin？

Admin是Django自带的一个功能强大的自动化数据库管理界面

被授权的用户可直接在Admin中管理数据库

Django提供了许多针对Admin的定制功能



### 配置Admin

#### 创建用户

**python manage.py createsuperuser** 创建超级用户

#### 访问后台管理系统

**localhost:8000/admin** Admin入口

修改**settings.py**中**LANGUAGE_CODE = 'zh-hans'**

#### 配置应用

在应用下**admin.py**中引用**自身的models**模块（或里面的模型类）

编辑admin.py：**admin.site.register(models.Article)**

#### 修改数据

点击Article超链接进入**Article列表页面**

点击任意一条数据，进入编辑页面修改

编辑页面下方一排按钮执行相应操作

#### 修改数据默认显示名称

在Article类下添加一个方法

根据Python版本选择

```python
__str__(self)或__unicode_(self)
return self.title
```

