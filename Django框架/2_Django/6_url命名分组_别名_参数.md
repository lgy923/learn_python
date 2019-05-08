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

