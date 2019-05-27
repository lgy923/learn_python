**login.html**

```django
<html>
    <body>
        {#<form action="/index/" method="post">#}
        <form action={% url "alex" %} method="post">
            {# alex是urls.py中路径的别名 #}
            <input type="text" name="username">
            <input type="password" name="pwd">
            <input type="submit" value="submit">
        </form> 
    </body>
</html>
```

**views.py**

```python
def index(request):
	if request.method == "POST":
		username=request.POST.get("username")
         # 取出html提交的数据
		pwd=request.POST.get("pwd")
		
		if username == "alex" and pwd == "123":
			return HttpResponse("登录成功！")
    return render(request, "login.html")
```

**urls.py**

```python
url(r'^index', views.index, name="alex")
# alex为这个url的别名
```



### URL，命名分组，无命名分组

**urls.py**

```python
from django.contrib import admin
from django.urls import path, re_path
from django.conf.urls import url

from blog import views

urlpatterns = [
    path(r'admin/', admin.site.urls),
    path(r'cur_time/', views.cur_time),
    # 通过正则表达式匹配字段
    # 第二个参数，字段与所执行的函数进行绑定（从views.py中导入）

    # 无命名分组
    url(r'^userinfo/$', views.user_info),
    url(r'^articles/([0-9]{4})/([0-9]{2})/$', views.year_archive),
    # 用括号括起来表示，作为值返回，需要用两个参数来接收，否则会报错

    # 有命名分组
    # path('articles/<int:y>/', views.year_archive),
    # path('articles/<int:y>/<int:m>/', views.year_archive),
    # 定义一个int型变量，接收该位置输入的字段

    # re_path(r'articles/(?P<y>[0-9]{4})/$', views.year_archive),
    # 用括号括起来表示，作为值返回，需要用一个参数来接收，否则会报错
]
```

**views.py**

```python
from django.shortcuts import render, HttpResponse
import datetime
from blog import models


def cur_time(request):

    times = datetime.datetime.now()
    # return HttpResponse("<h1>OK</>")
    return render(request, "cur_time.html", {"abc": times})  # 调用render方法进行渲染
    # 第一个参数必须是request
    # 第二个参数是目标html文件路径
    # 第三个参数是一个字典，运用模板语言，当html中遇到"abc"字段，则可传入times的值进行替换


def user_info(request):
    if request.method == "POST":
        u = request.POST.get("username", None)
        # 用一个变量获取前端提交的数据，通过相应字段（name属性）
        g = request.POST.get("gender", None)
        e = request.POST.get("email", None)

        # user = {
        #     "username": username,
        #     "gender": gender,
        #     "email": email
        # }

        # user_list.append(user)

        models.UserInfo.objects.create(
            username=u,
            # 把数据插入到数据库username字段中
            gender=g,
            email=e,
        )

    user_list = models.UserInfo.objects.all()
    return render(request, "index.html", {"user_list": user_list})


def year_archive(request, y=2005, m=3):
    # return HttpResponse("years")
    # return HttpResponse("{}year".format(y))
    return HttpResponse("{}year{}month".format(y, m))
```

