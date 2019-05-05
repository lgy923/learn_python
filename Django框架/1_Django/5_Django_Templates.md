### 什么是Templates

HTML文件

使用了Django模板语言（Django Temlates Language，DTL）

可以使用第三方模板（如Jinja2）

### 步骤

在应用下新建一个urls.py文件，把myblog中的urls.py内容复制过去，删掉不需要的内容

![](images/11.png)

在APP的根目录下创建名叫Templates的目录

![](images/6.png)

在该目录下创建HTML文件

![](images/7.png)

在views.py中返回一个render()

![](images/8.png)



在根urls.py中引入include

在APP目录下创建urls.py文件，格式与根urls.py相同

根urls.py中url函数第二个参数改为include('blog.urls')



注意事项

根urls.py针对APP配置URL名称，是该APP所有URL的总路径

配置URL时注意**正则表达式结尾符号** **$** 和 **/** 



### DTL初步使用

-   **render()**函数中支持一个**dict类型**参数
-   该字典是后台传递到模板的参数，**键为参数名**
-   在模板中使用{{ **参数名** }}来直接使用

![](D:/PythonProgram/python_rimi/learn_python/Django%E6%A1%86%E6%9E%B6/images/9.png)

![](D:/PythonProgram/python_rimi/learn_python/Django%E6%A1%86%E6%9E%B6/images/10.png)



### Django查找Templates

Django按照**INSTALLED_APPS中的添加顺序**查找Templates

不同APP下Templates目录中的同名.html文件会造成冲突

### 解决Templates冲突方案

在APP的Templates目录下创建以APP名为名称的目录

将html文件放入新创建的目录下

在新建Templates后，在templats文件目录下再新建一个**与应用同名**的文件目录，把html文件模板全部放入到新建的文件目录下

