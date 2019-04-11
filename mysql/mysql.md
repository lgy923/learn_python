<h1>Content</h1>

<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#基本命令">一、基本命令</a>

<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#基本表操作">二、数据表操作</a>



```
https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md
```



参考链接：https://juejin.im/post/5ae55861f265da0ba062ec71

<h2>基本命令</h2>

```mysql
-- 连接mysql服务器
mycli -u p1901 -h 10.2.1.78;
mysql -u p1901 -h 10.2.1.78 -p;
-- 退出客户端
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

-- 查看数据表结构
desc tb1;

-- 删除数据表
drop table tb1;  -- 删除数据表

-- 清空表内容
delete from tb1;  -- 清空tb1表中内容
truncate table tb1;  -- 清空tb1表中内容（与上者略有不同，速度快，自增回到原点）

-- 查看数据表
select * from user_user;  -- 查看user_user表
```

**注意**：数据库和数据表建议使用 **``** 号(键盘左上角数字1左边)括起来。  



<h2>数据表操作</h2>

<h3>术语概念</h3>
1、**auto_increment**：自增列（一张表只能有一个，数字，必须是索引-主键）

2、允许**null**值，则说明在插入数据的时候允许不给出该列的值；而**not null**则表示插入或者更新该列数据时必须给出该列的值。

3、**default**表示该列的默认值。在插入行数据时，若没有给出该列的值就会使用其指定的默认值。

4、**primary key**用于指定主键。主键可以指定一列数据，也可以由多列数据组成。如，primary key(cust_id,cust_name);主键的特性：i 不可以为空  ii 不能重复。

5、外键

6、**engine**用于指定引擎类型，常见的引擎类型：

　　i、InnoDB，是一个可靠的事物处理引擎，但是不支持全文本搜索。

　　ii、MyISAM是，是一个性能极高的引擎，它支持全文本搜索，但是不支持事物处理。

　　iii、MEMORY在功能上等同于MyISAM，但由于数据存储在内存中，速度很快（特别适合于临时表）。

　　参考：https://segmentfault.com/a/1190000012588602




<h3>表结构操作</h3>

```mysql
-- 创建数据表
create table `tb1`(  -- tb1数据表名称
    id int not null auto_increment primary key,  -- id属性，整数型，不能为空，自增，设为主键
    stu_name varchar(20) not null,  -- stu_name属性，字符串型，最长20字符，不能为空
    age int null default 18,  -- age属性，整形，可以为空，默认值18
    gender varchar(10),  -- gender属性，字符串型，最长10字符
    id_out int,
    primary key(id),  -- 设置id属性为主键
    foreign key (id_out) references `Persons`(id_out)
)engine=InnoDB charset=utf8;

-- 重命名表名
rename table tb1 to tb2;

-- 基本表新增列
alter table tb1 add hobby varchar(20);
```

**注释**：





<h3>表数据操作</h3>

**增加（插入）语句**

```mysql
insert into tb1 (stu_name,age,gender,telephone) values ('Culun',25,'male','213213131');

insert into tb1 values (16,'Culun',25,'male','213213131','basketball');
```



**删除语句**

```mysql
delete from tb1 where id is null;  -- 删除tb1表中id属性为空的元组
delete from tb1 where id = 15;  -- 删除tb1表中id=15的元组
```



**修改（更新）语句**

```mysql
update tb1 set age = 21 where id = 14;  -- 修改tb1表中id=14的age为21
```



**查询语句**

```mysql
select stu_name from tb1 where age=20;  -- 查看年龄为20的人员姓名
select distinct stu_name from tb1;  -- 为查出的stu_name列信息去重  
select stu_name from tb1 where age=20 limit 5;  -- 只查看5个age为20的姓名

子查询
select * from tb1 where age=(select max(age) from tb1);  -- 查看年纪最大的人所有信息

select class,count(*) from tb1 group by class;  -- 查看各个班的人数
select class,count(*) from tb1 group by class having class='b';

联表查询
select * from t1 join t2 where t1.i1=t2.i2;  -- 先进行表拼接，然后再筛选
select * from t1 join t2 on ti.i1=t2.i2;  -- 合并表的时候就筛选

select * from t1 left join t2 on ti.i1=t2.i2;  -- t1为主表匹配，没有匹配到的null
```

**过滤条件操作符有**：

```
<=>，=，<，!=，<=，>，>=，between and，is null。
```



<h2>用户权限</h2>

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



**数据库五种关系代数运算**：

```

```

