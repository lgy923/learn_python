urls.py

```python
from django.contrib import admin
from django.urls import path
from django.conf.urls import url
from app01 import views

urlpatterns = [
    path('admin/', admin.site.urls),
    url(r'index/', views.index),
]
```

index.html

```django
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h1>Template</h1>

{#{{ list.2 }}  {# 333 #}
{#{{ dict1.three }}  {# 3 #}
{# 用.代替[]来索引值 #}

{#{{ time1.year }}  {# 2019 #}
{#{{ time1.month }}  {# 5 #}
{# 调用属性时，还是用.来调用 #}

{#{{ person1.name }}#}
{#{{ person1.age }}#}

{#{% if 1 %}#}
{#    <p>hello world</p>  {# hello world #}
{#{% elif person1 %}#}
{#    <p>hello python</p>#}
{#{% endif %}#}

{#{% for i in list %}#}
{#    <p>{{ forloop.counter }}:{{ i }}</p>#}
{#    forloop.counter从1开始计数#}
{#{% endfor %}#}

{#{% for i in list %}#}
{#    <p>{{ forloop.counter0 }}:{{ i }}</p>#}
    {# forloop.counter从0开始计数#}
{#{% endfor %}#}

{#{% for i in dict1 %}#}
{#    <p>{{ i }}</p>#}
{#{% endfor %}#}

{#{{ hello }}  {# hello #}
{#{{ hello|upper }}  {# HELLO #}
{#通过管道符调用upper使全字母大写#}
{#{{ hello|lower }}  {# hello #}
{#{{ hello|capfirst}}  {# Hello #} {# 首字母大写 #}

{#{{ s6|add:5 }}  {# 11 #}
{#通过管道符调用add方法，在冒号后面写加的数#}

{#{{ s7|default:"空" }}  {# 空 #}
{#如果s7为空，则显示default后面的值，如果不为空，则显示本身的值#}

{#{{ s8 }}  {# <a href="#">跳转</a> #}
{# 虽然浏览器可以识别s8字符转中的a标签，但是出于安全考虑，没有对其进行渲染 #}

{#{% autoescape off %}#}
{#    {{ s8 }}#}
{#{% endautoescape %}#}
{# 通过autoescape对s8字符串进行控制，使得浏览器会对其进行渲染成为超链接效果 #}

{#{{ s8|safe }}  {# 效果与autoescape一样 #}

</body>
</html>
```

views.py

```python
from django.shortcuts import render
import datetime


def index(request):

    class Person:
        def __init__(self, name, age):
            self.name = name
            self.age = age

    s = "hello"
    s2 = [1, 22, 333]
    s3 = {"one": 1, "two": 2, "three": 3}

    s4 = datetime.datetime.now()
    s5 = Person('alex', 18)

    s6 = 6
    s7 = []

    s8 = '<a href="#">跳转</a>'

    # return render(request, "index.html", {"list": s2})
    # return render(request, "index.html", {"dict1": s3})
    # return render(request, "index.html", {"time1": s4})
    # return render(request, "index.html", {"person1": s5})
    # return render(request, "index.html", {"hello": "hello"})
    # return render(request, "index.html", {"s6": s6})
    # return render(request, "index.html", {"s7": s7})
    return render(request, "index.html", {"s8": s8})
```

