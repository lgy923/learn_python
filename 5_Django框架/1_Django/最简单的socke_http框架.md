```python
# -*- coding:utf-8 -*-
# @Author:Liu Guoyang
# @Time  :2019/5/5 16:05
# @File  :server_socket.py

import socket


def handle_request(conn):
    data_recv = conn.recv(65535)

    with open("2_3.html", 'rb') as f:
        data = f.read()

    conn.send("HTTP/1.1 200 OK\r\n\r\n".encode("utf8"))
    conn.send(data)


def main():
    address = ('127.0.0.1', 8003)
    server = socket.socket()
    server.bind(address)
    server.listen(5)
    print("服务端已启动...")

    while True:
        conn, addr = server.accept()
        print("{}已连接至服务端".format(addr))
        handle_request(conn)


if __name__ == '__main__':
    main()
```

