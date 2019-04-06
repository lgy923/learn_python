<h2>1、socket实现基本服务端和客户端基本通信</h2>

**服务端**

```python
# -*- coding:utf-8 -*-

import socket  # 导入socket模块

address = ('127.0.0.1', 55556)  # 设置服务端IP地址和端口号

server = socket.socket()  # 初始化socket
server.bind(address)  # socket绑定服务端地址
server.listen(5)  # 监听客户端，并设置最大排队等候连接的客户端数量

conn, addr = server.accept()  # 连接客户端，conn接收客户端对象，addr接收客户端地址和端口号
data_recv = conn.recv(65535)  # 接收数据，并设置单次最大接收数据大小，单位byte（字节）

print(data_recv.decode())  # 显示接收的数据，传输的数据时二进制格式，所以需要先转码
# print(str(data_recv, 'utf8'))  # 转换成str格式再打印输出（与上一句功能一样）
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
```

注意：

i、发送和接收的数据的格式都是二进制类型。encode()方法编码，decode()解码。

ii、服务端使用的端口号自定义，建议使用30000~65535之间的端口号。



<h2>2、socket实现服务端和客户端</h2>