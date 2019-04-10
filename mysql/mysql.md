<h3>基本命令</h3>

```mysql
-- 连接mysql服务器
mycli -u p1901 -h 10.2.1.78
mysql -u p1901 -h 10.2.1.78 -p
-- 推出客户端
exit

-- 创建数据库
create database db1  -- 创建名为db1数据库

-- 删除数据库
drop database db1 -- 删除db1数据库

-- 进入数据库
use django1  -- 进入django1数据库

-- 查看基本表
select * from user_user  -- 查看user_user表

-- 创建基本表
create table tb1(  -- tb1基本表名称
    id int not null primary key,  -- id属性，整数型，不能为空，设为主键
    stu_name varchar(20) not null,  -- stu_name属性，字符串型，最长20字符，不能为空
    age int,  -- age属性，整形
    gender varchar(10)  -- gender属性，字符串型，最长10字符
)engine=InnoDB;
```