## Redis安装与基本配置

### 安装

#### Windows

下载链接：https://github.com/microsoftarchive/redis/releases/download/win-3.0.504/Redis-x64-3.0.504.msi

打开命令窗口，运行服务端：**redis-server.exe redis.windows.conf**

新建一个终端：**redis-cli**

测试安装是否成功：**ping**

#### MacOS

下载链接：http://download.redis.io/releases/redis-5.0.5.tar.gz

解压gz文件：**tar xzf redis-5.0.5.tar.gz**

进入到redis目录：**cd redis-5.0.5**

make编译：**make**

进入到src目录：**cd src**

运行redis服务(通过默认参数启动)：**./redis-server**

新建一个终端，进入到src目录下：**cd redis-5.0.5/src**

启动客户端连接到服务端：**./redis-cli -h 127.0.0.1 -p 6379**

#### Ubuntu

升级apt工具：**apt-get update**

安装redis：**sudo apt-get install redis-server**

运行服务端：**redis-server**

新建一个终端：**redis-cli**



### 停止redis服务

#### Ubuntu

开启redis服务：**sudo service redis start**

关闭redis服务：**sudo service redis stop**

查看进程：**ps -ef | grep redis**

#### Windows

以**管理员身份**运行cmd

开启redis服务：**net redis stop**

关闭redis服务：**net redis start**

#### MacOS

开启redis服务：**./redis-server**

关闭redis服务：**kill -9** *pid*



### 配置

打开**redis.conf**文件（windows是**redis.windows.conf**）

修改IP地址：**bind 127.0.0.1**

修改端口号：**port 6379**

守护进程（可以在后台运行）：**daemonize yes**

设置日志级别：**loglevel notice**

默认数据库个数，默认是16(0-15)个，数据库没名字：**database 16**

从内存把数据写入到物理硬盘的频度：**save 900 1**（内存中900s执行了1次写操作，那就执行一次写入硬盘的操作）

物理存储文件的名字：**dbfilename dump.rdb**

默认存储的位置：**dir /var/lib/redis**









