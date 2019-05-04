### wsgi.py

WSGI（Python Web Server Gateway Interface）：Python服务器网关接口

Python应用与Web服务器之间的接口



### *urls.py

URL配置文件，Django项目中所有地址（页面）都需要我们自己去配置其URL



### *setting.py

项目的总配置文件，里面包含了数据库、web应用、时间等各种配置

-   BASE_DIR：指的项目的根目录
-   DEBUG：开启，会把异常抛出给用户
-   ALLOWED_HOSTS = ['localhost']，只允许用户通过localhost访问
-   INSTALLED_APPS：安装的应用
-   MIDDLEWARE:django自带的工具集
-   TEMPLATES：模板
-   DATABASES：数据库配置
-   LANGUAGE_CODE：语言（默认美式英语）
-   STATIC_URL：静态文件地址



### __init__.py

声明模块的文件,内容默认为空