<h3>基本命令</h3>

```mysql
-- 连接mysql服务器
mycli -u p1901 -h 10.2.1.78;
mysql -u p1901 -h 10.2.1.78 -p;
-- 推出客户端
exit;

-- 创建数据库
create database `db1`;  -- 创建名为db1数据库

-- 查看数据库状态
show status;

-- 删除数据库
drop database `db1`; -- 删除db1数据库

-- 进入数据库
use django1;  -- 进入django1数据库

-- 查看当前数据库中所有可用的表
show tables;
```

**注意**：数据库和基本表建议使用 **``**号(不是引号)括起来。  

<h3>基本表操作</h3>

```mysql
-- 查看基本表
select * from user_user;  -- 查看user_user表

-- 创建基本表
create table `tb1`(  -- tb1基本表名称
    id int not null primary key,  -- id属性，整数型，不能为空，设为主键
    stu_name varchar(20) not null,  -- stu_name属性，字符串型，最长20字符，不能为空
    age int null default 18,  -- age属性，整形，可以为空，默认值18
    gender varchar(10),  -- gender属性，字符串型，最长10字符
    id_out int,
    primary key(id),
    foreign key (id_out) references `Persons`(id_out)
)engine=InnoDB;

-- 重命名表名
rename table tb1 to tb2;

-- 基本表新增列
alter table tb1 add hobby varchar(20);
```

注释：

1、允许**null**值，则说明在插入数据的时候允许不给出该列的值；而**not null**则表示插入或者更新该列数据时必须给出该列的值。

2、**default**表示该列的默认值。在插入行数据时，若没有给出该列的值就会使用其指定的默认值。

3、**primary key**用于指定主键。主键可以指定一列数据，也可以由多列数据组成。如，primary key(cust_id,cust_name);主键的特性：i 不可以为空  ii 不能重复。

4、**engine**用于指定引擎类型，常见的引擎类型：

　　i、InnoDB，是一个可靠的事物处理引擎，但是不支持全文本搜索。

　　ii、MyISAM是，是一个性能极高的引擎，它支持全文本搜索，但是不支持事物处理。

　　iii、MEMORY在功能上等同于MyISAM，但由于数据存储在内存中，速度很快（特别适合于临时表）。



<h3>用户权限</h3>

```mysql
-- 创建用户
create user lgy1@'%' identified by '123456';

-- 删除用户
drop user lgy2@'%';
drop user lgy2@ 127.0.0.1；

-- 用户授权
grant all privileges on *.* to lgy1@'%';  -- 授予用户lgy1所有数据库的所有权限
grant select on *.* to lgy1@'%';  -- 授予用户lgy1所有数据库的select权限
grant select, insert on database1.* to lgy4@'%';  -- 授予用户lgy4数据库database1的select和insert权限

-- 刷新权限信息表
flush privileges;
```

**注意**：授权的IP地址要和创建用户时的IP一致。