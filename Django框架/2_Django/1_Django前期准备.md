### 通过socket实现简单的http请求服务器且返回数据

```python
# -*- coding:utf-8 -*-
# @Author:Liu Guoyang
# @Time  :2019/5/5 16:05
# @File  :server_socket.py

import socket


def handle_request(conn):
    data_recv = conn.recv(65535)  # 接收浏览器的请求报文
    # print(data_recv)

    # with open("2_3.html", 'rb') as f:
    #     data = f.read()

    data = b"hello world!"

    conn.send("HTTP/1.1 200 OK\r\n\r\n".encode("utf8"))  # 发送http报文头信息，表示以网页的形式在浏览器上展示
    conn.send(data)  # 需要在浏览器上展现的内容


def main():
    address = ('127.0.0.1', 8080)
    server = socket.socket()
    server.bind(address)
    server.listen(5)
    print("服务端已启动...")

    while True:
        conn, addr = server.accept()  # 等待浏览器（客户端）请求
        print("{}已连接至服务端".format(addr))
        handle_request(conn)  # 当有客户端接入（及有浏览器发送请求）时，执行handle_request函数


if __name__ == '__main__':
    main()
```

开启服务（运行该程序），然后在浏览器中输入： **127.0.0.1:8080**



### 通过python内置的WSGI（Web Server Gateway Interface）服务器，简化上述代码，实现相同功能

```python
# -*- coding:utf-8 -*-
# @Author:Liu Guoyang
# @Time  :2019/5/5 16:27
# @File  :server2.py

from wsgiref.simple_server import make_server


def application(environ, start_response):
    # 通过environ封装成一个所有请求信息的对象
    start_response('200 OK', [('Content-Type', 'text/html')])
    # start_response可以很方便地设置响应头
    return [b'<h1>Hello, web!</h1>']


# 封装了socket对象以及准备过程（socket，bind，listen）
httpd = make_server('', 8080, application)  # 实例化一个httpd对象

print('Serving HTTP on port 8080...')
httpd.serve_forever()  # 通过实例化的这个对象调用serve_forever方法
```

开启服务（运行该程序），然后在浏览器中输入： **127.0.0.1:8080**



### 升级上述代码。

```python
# -*- coding:utf-8 -*-
# @Author:Liu Guoyang
# @Time  :2019/5/5 19:56
# @File  :server3.py

from wsgiref.simple_server import make_server


def application(environ, start_response):
    # 通过environ封装成一个所有请求信息的对象
    # print("environ", environ)
    # print("environ['PATH_INFO']", environ["PATH_INFO"])

    start_response('200 OK', [('Content-Type', 'text/html')])
    # start_response可以很方便地设置响应头

    path = environ["PATH_INFO"]

    if path == '/book':
        return [b'<h1>Hello, book!</h1>']
        # 当浏览器中输入127.0.0.1:8003/book时，返回Hello，book！

    elif path == '/web':
        return [b'<h1>Hello, web!</h1>']

    else:
        return [b"<h1>404</h1>"]
        # 当浏览器中输入除上述两种情况时，返回404


# 封装了socket对象以及准备过程（socket，bind，listen）
httpd = make_server('', 8080, application)

print('Serving HTTP on port 8080...')
httpd.serve_forever()
```

-   当在浏览器中输入：127.0.0.1:8003/web时，返回Hello book！
-   当在浏览器中输入：127.0.0.1:8003/web时，返回Hello web！
-   当在浏览器中输入上述两种除外的情况时，返回404！



### 升级上述代码。

```python
# -*- coding:utf-8 -*-
# @Author:Liu Guoyang
# @Time  :2019/5/5 20:10
# @File  :server4.py

from wsgiref.simple_server import make_server


def f1(request):
    return [b'<h1>Hello, book!</h1>']


def f2(request):
    return [b'<h1>Hello, web!</h1>']


def f3(request):
    return [b'<h1>404</h1>']


def login(request):
    # print(request)
    return [b"<h1>hello login</h1>"]


def routers():
    urlpatterns = (
        ('/book', f1),  # 如果匹配到/book则执行f1函数
        ('/web', f2),
        ('/login', login),
    )
    return urlpatterns


def application(environ, start_response):

    start_response('200 OK', [('Content-Type', 'text/html')])
    path = environ["PATH_INFO"]  # path==/web

    urlpatterns = routers()  # 接收routers返回的值，得到一个元组
    func = None  # 初始化func变量，准备接收函数作为值

    for item in urlpatterns:
        if item[0] == path:  # 如果元组中第一个元素等于浏览器请求的域名段
            func = item[1]
            break

    if func:  # 如果func有值，则执行这个函数
        return func(environ)
    else:  # 如果func为空，则返回404
        return [b"<h1>404</h1>"]


httpd = make_server('', 8080, application)

print('Serving HTTP on port 8080...')
httpd.serve_forever()
```



### 在一个html页面中显示当前时间

**current_time.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>current_time</title>
</head>
<body>

<h1>
    current_time: !cur_time!  <!-- 通过模板语言标记字段-->
</h1>

</body>
</html>
```

**server.py**

```python
# -*- coding:utf-8 -*-
# @Author:Liu Guoyang
# @Time  :2019/5/5 20:52
# @File  :server5.py

from wsgiref.simple_server import make_server
import time  # 导入时间模块


def current_time(request):
    f = open("current_time.html", 'rb')  # 打开current_time.html文档
    data = f.read()  # 把html文档中数据存储到变量data中

    cur_time = time.ctime(time.time())  # 创建一个时间戳，并产生当前时间
    data = str(data, "utf8").replace("!cur_time!", cur_time)
    # 通过 模板语言 把html文档中的 !cur_time! 部分替换为当前获取到的时间

    return [data.encode()]  # 转码后返回替换


def routers():
    urlpatterns = (
        ('/current_time', current_time),  # 当浏览器请求到/current_time字段时，执行current_time函数
    )
    return urlpatterns


def application(environ, start_response):

    start_response('200 OK', [('Content-Type', 'text/html')])  # HTTP请求头
    path = environ["PATH_INFO"]  # path==/web

    urlpatterns = routers()  # 接收routers返回的值
    func = None  # 初始化func变量，准备接收函数作为值

    for item in urlpatterns:
        if item[0] == path:  # 如果元组中第一个元素等于浏览器请求的域名段
            func = item[1]
            break

    if func:  # 如果func有值，则执行这个函数
        return func(environ)
    else:  # 如果func为空，则返回404
        return [b"<h1>404</h1>"]


httpd = make_server('', 8080, application)

print('Serving HTTP on port 8080...')
httpd.serve_forever()
```

