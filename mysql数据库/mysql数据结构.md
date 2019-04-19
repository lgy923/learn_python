<h3>存储过程</h3>

**创建存储过程**

```mysql
delimiter $  -- 重新定义定界符

create procedure p1()  # 创建存储过程
begin -- 存储过程开始
select * from `Student`;  -- 存储过程体
end$  -- 存储过程结束

delimiter ;  -- 把；重新定义为定界符

call p1;  -- 执行存储过程
```



触发器

```mysql
create trigger t_test1 
before insert on `Employee` for each begin NEW.salary=50;end$
```



事件

```mysql
create event salary_up on schedule  -- 创建事件
every 5 second  -- 每5秒执行一次
do update `Employee`   -- 执行的内容是（修改`Employee`表）
set salary=salary+5;  -- 把`salary`增加5
```

