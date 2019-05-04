### Django中的Models是什么？

-   通常，**一个Model**对应的数据库的一张数据表
-   Django中Models以**类**的形式表现
-   它包含了一些**基本字段**以及数据的**一些行为**



### ORM（Object Relation Mapping）：对象关系映射

实现了**对象和数据库**之间的**映射**

隐藏了数据访问的细节，**不需要编写SQL语句**



### 编写Models

-   在应用根目录下创建models.py，并引入models模块
-   创建类，继承models.Models，该类即是一张数据表
-   在类中创建字段

 

#### 创建字段

字段即类里面的属性（变量）

attr = CharField(max_length=64)

#### 生成数据表

命令行中进入**manage.py同级目录**

执行**python manage.py makemigrations add名**（可选）

再执行**python manage.py migrate**

#### 查看

Django会自动在**app/migrations/**目录下生成移植文件

执行**python mange.py sqlmigrate 应用名 文件id** 查看sql语句

**默认sqlite3**的数据库在项目根目录下**db.sqlite3**

#### 页面呈现数据

后台步骤

views.py中import models

article = models.Article.bojects.get(pk=1)

render(request,page,{'article': article})

前端步骤

模板可直接使用对象以及对象的“.”操作

**{{ article.title }}**