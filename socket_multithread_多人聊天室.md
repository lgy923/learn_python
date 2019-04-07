```
实现一个多人聊天系统（类似于QQ群），一个客户端发送消息，经过服务端广播，其他客户端都可以收到消息。
```

<h2>1、socket实现服务端和客户端基本通信</h2>

**服务端**

```python
# -*- coding:utf-8 -*-

import socket  # 导入socket模块

address = ('127.0.0.1', 55556)  # 设置服务端IP地址和端口号

server = socket.socket()  # 初始化socket
server.bind(address)  # socket绑定服务端地址
server.listen(5)  # 监听客户端，并设置最大排队等候连接的客户端数量

conn, addr = server.accept()  # 连接客户端，conn接收客户端对象，addr接收客户端地址和端口号
print("{}已连接至服务端...".format(addr))  # 提示客户端已连接

data_recv = conn.recv(65535)  # 接收数据，并设置单次最大接收数据大小，单位byte（字节）

print(data_recv.decode())  # 显示接收的数据，传输的数据时二进制格式，所以需要先转码
# print(str(data_recv, 'utf8'))  # 转换成str格式再打印输出（与上一句功能一样）

conn.close()  # 关闭连接的客户端
server.close()  # 关闭服务端
```

**客户端**

```python
# -*- coding:utf-8 -*-

import socket  # 导入socket模块

server_address = ('127.0.0.1', 55556)  # 要连接的服务端IP地址和端口号

client = socket.socket()  # 初始化socket
client.connect(server_address)  # 连接服务端

input_msg = input("请输入消息：")  # 键盘输入发送的消息内容
client.send(input_msg.encode())  # 发送消息，需要把str格式转换成二进制格式的数据再传输
# client.send(bytes(input_msg, 'utf8'))  # 转换成二进制格式再传输（与上一句功能一样）

client.close()  # 关闭客户端
```

**注意：**

i、发送和接收的数据的格式都是二进制类型。encode()方法编码，decode()解码。

ii、服务端使用的端口号自定义，建议使用30000~65535之间的端口号。



<h2>2、socket实现服务端和客户端长时间通信</h2>

尽管实现了服务端和客户端通信，但是我们发现，仅仅是客户端发送消息，服务端收消息，并且收发一条消息后就会退出。我们要实现，当客户端想要退出时才退出。

**服务端**

```python
# -*- coding:utf-8 -*-

import socket

address = ('127.0.0.1', 55556)

server = socket.socket()
server.bind(address)
server.listen(5)

conn, addr = server.accept()
print("{}已连接至服务端...".format(addr))  # 提示客户端已连接

while True:  # 重复接受消息

    data_recv = conn.recv(65535)

    if not data_recv.decode():  # 如果客户端发送的消息为空，则不再接受消息
        print("{}已连接断开连接...".format(addr))  # 提示客户端已断开连接
        break

    print(data_recv.decode())

server.close()
```

**客户端**

```python
# -*- coding:utf-8 -*-

import socket

server_address = ('127.0.0.1', 55556)

client = socket.socket()
client.connect(server_address)

while True:  # 重复发送消息
    input_msg = input("请输入消息：")

    client.send(input_msg.encode())

    if not input_msg:  # 如果输入的内容为空，则退出通信
        break

client.close()
```

为了代码模块化，功能结构更清晰，我们把功能模块用函数来表示。

**服务端_函数表示**

```python
import socket


def server_recv(conn, addr):  # 接收消息函数
    while True:  # 重复接受消息
        data_recv = conn.recv(65535)

        if not data_recv.decode():  # 如果客户端发送的消息为空，则不再接受消息
            print("{}已连接断开连接...".format(addr))  # 提示客户端已断开连接
            break

        print(data_recv.decode())


def server_handle(address):  # 主题配置，监听和连接客户端
    server = socket.socket()
    server.bind(address)
    server.listen(5)

    conn, addr = server.accept()
    print("{}已连接至服务端...".format(addr))  # 提示客户端已连接

    server_recv(conn, addr)  # 调用接收消息的函数

    server.close()


if __name__ == '__main__':
    server_address = ('127.0.0.1', 55556)
    server_handle(server_address)
```

**客户端_函数表示**

```python
# -*- coding:utf-8 -*-

import socket


def client_send(address):
    client = socket.socket()
    client.connect(address)

    while True:  # 重复发送消息
        input_msg = input("请输入消息：")

        client.send(input_msg.encode())

        if not input_msg:  # 如果输入的内容为空，则退出通信
            break

    client.close()


if __name__ == '__main__':
    server_address = ('127.0.0.1', 55556)
    client_send(server_address)
```



<h2>3、socket和<a href="https://github.com/lgy923/learn_python/blob/master/%E5%A4%9A%E8%BF%9B%E7%A8%8B.md">多线程</a>实现多个客户端可以同时向服务端发送消息</h2>

**服务端**

```python
# -*- coding:utf-8 -*-

import socket
from threading import Thread  # 导入threading模块


def server_recv(conn, addr):
    while True:  # 重复接受消息
        data_recv = conn.recv(65535)

        if not data_recv:  # 当收到的消息为空时，表示客户端断开连接
            print("用户{}已断开连接".format(addr))
            break

        print(data_recv.decode())


def server_handle(address):
    
    server = socket.socket()
    server.bind(address)
    server.listen(3)

    while True:

        conn, addr = server.accept()
        print("用户{}已连接至服务端".format(addr))

        handle = Thread(target=server_recv, args=(conn, addr))  # 创建线程

        handle.start()  # 开启线程

        conn.close()


if __name__ == '__main__':
    server_address = ('127.0.0.1', 55666)
    server_handle(server_address)
```

server_handle函数中while循环中的语句，当执行到conn, addr = server.accept()部分时会发生阻塞，即除非有客户端连接进来，才会往下执行，如果一直客户端连接进来，则不会执行接收消息的语句。此时，就可以创建一个线程，使用**多线程**来解决这个问题。

代码都是从上往下顺序执行的。由于阻塞，会影响到后面代码得执行。所以多进程可以实现多个程序块“同时执行”，即便是conn, addr = server.accept()阻塞暂停了程序，但是后面创建的进程所指向的程序块还是可以执行。

**客户端**

```python
# -*- coding:utf-8 -*-

import socket


def client_send(address):
    client = socket.socket()
    client.connect(address)

    while True:
        input_msg = input(">>>")
        client.send(input_msg.encode())

        if not input_msg:
            break
    
    client.close()
    

if __name__ == '__main__':
    server_address = ('127.0.0.1', 55666)
    client_send(server_address)
```

