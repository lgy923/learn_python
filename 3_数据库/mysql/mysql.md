<h1>Content</h1>

<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#基本命令">一、基本命令</a>

<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#数据表操作">二、数据表操作</a>

　　<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#术语概念">(一)术语概念</a>

　　<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#表结构操作">(二)表结构操作</a>

　　<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#表数据操作">(三)表数据操作</a>

　　　　<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#增加数据">1、增加(插入数据)</a>

　　　　<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#删除数据">2、删除数据</a>

　　　　<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#修改数据">3、修改数据</a>

　　　　<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#查询数据">4、查询数据(重难点)</a>

　　<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#过滤条件操作符">(四)过滤条件操作符</a>

<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#用户权限">三、用户权限</a>

<a href="https://github.com/lgy923/learn_python/blob/master/mysql/mysql.md#数据库五种关系代数运算">四、数据库五种关系代数运算</a>



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
drop table tb1;

-- 清空表
delete from tb1;  -- 仅清空tb1表中内容
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

4、**primary key**用于指定主键。主键可以指定一列数据，也可以由多列数据组成。如，primary key(cust_id,cust_name)；

　　主键的特性：i 不可以为空  ii 不能重复。

5、**foreign key**用于两张表建立约束，可一对多。如，foreign key (id_out) references `Persons`(id_out)；

6、**engine**用于指定引擎类型，常见的引擎类型：

　　i、InnoDB，是一个可靠的事物处理引擎，但是不支持全文本搜索。

　　ii、MyISAM是，是一个性能极高的引擎，它支持全文本搜索，但是不支持事物处理。

　　iii、MEMORY在功能上等同于MyISAM，但由于数据存储在内存中，速度很快（特别适合于临时表）。

　　MySQL引擎参考：https://segmentfault.com/a/1190000012588602




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
)engine=InnoDB charset=utf8;  -- 设置引擎（engine）和编码格式（charset）

-- 重命名表名
rename table tb1 to tb2;  -- 把tb1表重命名为tb2

-- 基本表新增列
alter table tb1 add hobby varchar(20);  -- 在tb1表中新增hobby属性
alter table tb1 drop hobby varchar(20);  -- 删除tb1表中删除hobby属性

-- 添加主键
alter table tb1 add primary key(id);  -- 添加tb1表中id列为主键

-- 删除主键
alter table tb1 drop primary key(id);  -- 删除tb1表中id列的主键

-- 添加外键
alter table tb1 add constraint fk1 foreign key student(depart_id) references department(dep_id);  -- 添加名为fk1的外键，表student的depart_id列和department的dep_id列 

-- 删除外键
alter table student drop foreign key fk1;  -- 从student表删除外键fk1

-- 修改默认值
alter table student alter stu_weight set default 75;  -- 修改表student中stu_weight列的默认值为75

-- 删除默认值
alter table student alter stu_weight drop default;  -- 删除student表中stu_weight列的默认值
```



<h3>表数据操作</h3>

<h5>增加数据</h5>

```mysql
insert into tb1 (stu_name,age,gender,telephone) values ('Culun',25,'male','213213131');  -- 选择具体属性插入对应数据
insert into tb1 values (16,'Culun',25,'male','213213131','basketball');  -- 此种插入数据的方法必须逐个插入所有属性的数据
```



<h5>删除数据</h5>

```mysql
delete from tb1 where id is null;  -- 删除tb1表中id属性为空的元组
delete from tb1 where id = 15;  -- 删除tb1表中id=15的元组
```



<h5>修改数据</h5>

```mysql
update tb1 set age = 21 where id = 14;  -- 修改tb1表中id=14的age为21
```



<h5>查询数据</h5>

```mysql
select stu_name from tb1 where age=20;  -- 查看年龄为20的人员姓名
select distinct stu_name from tb1;  -- 为查出的stu_name列信息去重  
select stu_name from tb1 where age=20 limit 5;  -- 只查看5个age为20的姓名

-- 子查询
select * from tb1 where age=(select max(age) from tb1);  -- 查看年纪最大的人所有信息

select class,count(*) from tb1 group by class;  -- 查看各个班的人数
select class,count(*) from tb1 group by class having class='b';

-- 联表查询
select * from t1 join t2 where t1.i1=t2.i2;  -- 先进行表拼接，然后再筛选
select * from t1 join t2 on ti.i1=t2.i2;  -- 合并表的时候就筛选

select * from t1 left join t2 on ti.i1=t2.i2;  -- t1为主表匹配，没有匹配到的null

-- 排序查看
select * from employee order by salary desc;  -- 以salary列降序查看employee表所有数据
select * from employee order by salary asc;  -- 以salary升序查看employee表所有数据

-- ifnull用法
select ifnull(null, 'null')

select email from person group by email having count(*)
```



<h3>过滤条件操作符</h3>

```
<=>，=，<，!=，<=，>，>=，between and，is null。
```



<h2>用户权限</h2>

```mysql
-- 创建用户
create user lgy1@'%' identified by '123456';

-- 删除用户
drop user lgy2@'%';
drop user lgy2@127.0.0.1；

-- 用户授权
grant all privileges on *.* to lgy1@'%';  -- 授予用户lgy1所有数据库的所有权限
grant select on *.* to lgy1@'%';  -- 授予用户lgy1所有数据库的select权限
grant select, insert on database1.* to lgy4@'%';  -- 授予用户lgy4数据库database1的select和insert权限

-- 刷新权限信息表
flush privileges;
```

**注意**：授权的IP地址要和创建用户时的IP一致。



<h2>数据库五种关系代数运算</h2>

```

```





MySQL基础命令可参考链接：https://juejin.im/post/5ae55861f265da0ba062ec71

