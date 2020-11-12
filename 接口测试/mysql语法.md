#### MYSQL连接

##### 二进制方式连接

```html 
mysql -u root -p
再输入密码 *****
```

![image-20201019104649107](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201019104649107.png)

##### 使用php脚本连接

```php
mysqli_connect(host,username,password,dbname,port,socket)
/*
host:可选。规定主机名或ip地址
username：可选：规定mysql用户名
password：可选：规定mysql
dbname:可选。规定默认使用的数据库
port:可选。规定尝试连接到mysql服务器的端口号
socket:可选。规定socket或要使用的已命名pipe
```

#### MYSQL创建数据库

可在启动并登陆mysql服务后，使用create命令创建数据库

```php
mysql> create database stu;   //创建数据库
mysql> show databases;       //查看数据库
```

![image-20201019115258375](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201019115258375.png)

#### MYSQL删除数据库

**drop命令格式**

```php 
mysql> drop database stu; //删除数据库stu
```

![image-20201019142612364](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201019142612364.png)

#### MYSQL选择数据库

```php
mysql>use stu //执行此命令后，，后续操作都只在选择的stu数据库中
```

#### MYSQL创建数据表

需要以下信息：

- 表名
- 表字段名
- 定义每个表字段

**语法**

```mysql
create table tableName(column_name column_type);
```

```mysql
create table if not exists student(
id int UNSIGNED PRIMARY KEY auto_increment,
classname VARCHAR(100) not null,
age int UNSIGNED,
height decimal(5,2))
-- not null 代表输入该字段的数据为null时，会报错
-- auto_increment定义为自增的属性，一般用于主键，数值会主动加1
-- primary key用于定义列为主键
```

![image-20201019155913966](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201019155913966.png)

#### MYSQL删除数据表

**语法**

```mysql
drop table 表名
```

```mysql
drop table user
```

![image-20201019160511419](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201019160511419.png)

#### mysql插入数据

**语法**

**1.添加一行数据**

```mysql
insert into table_name (field1,field2,...)                                    values
                       (value1,value2,...)
```

```mysql
insert into student(classname,age,height)
                    VALUES
				   ('5班',18,167.23)
```

![image-20201020105412698](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201020105412698.png)

**2.添加多行数据**

```mysql
设置全部字段：
insert into table_name values
(value1,value2,value3,...),
(value1,value2,value3,...),
...
(value1,value2,value3,...)
```

```mysql
insert into student values(null,'4班',16,167.23),
                          (null,'3班',17,169)
```

```mysql
设置部分字段：
insert into table(fileds) values (value),(value),(value)
```

```mysql
insert into student (classname) values ('1班'),('2班'),('3班')
```

![image-20201020150522086](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201020150522086.png)

#### MYSQL查询数据

**语法：**

```mysql
select column_name,column_name
from table_name
[where clause]
[limit n][offset m]
```

**查询所有字段**

```mysql
select * from 表名
```

**查询指定字段**

```mysql
1>select field1,field2 from 表名
2>select name as 姓名,sex as 性别 from 表名
3>select s.name,c.age from stu as s,class as c
```

**消除重复行**                                         

```mysql
-- 在select后面，列前面使用distinct可以消除重复的行
select distinct 列1，... from 表名
```

```mysql
select distinct classname from student
```

![image-20201020153028980](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201020153028980.png)

#### MySQL WHERE  条件语句

语法：

```mysql
SELECT field1, field2,...fieldN FROM table_name1, table_name2...
[WHERE condition1 [AND [OR]] condition2.....
```

#### MySQL UPDATE 更新数据

更新修改数据库数据

**语法**

```mysql
update table_name set field1=new-value1, field2=new-value2
[WHERE Clause]
```

```mysql
update student set classname = '4班' where id = 5
```

#### MySQL DELETE 删除数据

```mysql
delete from table_name [where clause]
-- 如果没有指定where，mysql表中所有数据都该被删除
```

#### MySQL LIKE 模糊查询

% 表示任意多个字符

— 表示一个任意字符

**语法**

```mysql
select field1,field2 from table where field1 like condition1 [AND [OR]] field2 = 'somevalue'
```

```mysql
select * from student where classname like "%班"
```

#### MYSQL UNION 操作符

用于连接两个以上的select语句的结果到一个结果集合中 ，多个select语句会删除重复的数据。

**union all是把结果集直接合并在一起**

**union是将union all后的结果镜像一次distinct，去除重复的记录后的结果**

**语法**

```mysql
select expression1, expression2, ... expression_n
from tables
[where conditions]
union [all | distinct]
select expression1, expression2, ... expression_n
from tables
[where conditions];
```

```mysql
select classname from student UNION ALL select classname from class
select classname from student union select classname from class
```

![image-20201022144414687](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201022144414687.png)

#### MYSQL  ORDER BY 排序

**语法**

```mysql
select field1,field2,...fieldN from table_name1,table_names... order by field1 [ASC [desc][默认 ASC]]
```

```mysql
select * from student order by classname asc
-- asc指正序，desc指反序
```

![image-20201022150456473](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201022150456473.png)

#### MYSQL  GROUP  BY 分组

根据一个或多个列对结果集进行分组汇总

在分组的列上我们可以使用count，sum，avg等聚合函数

语法

```mysql
select column_name,function(column_name)
from table_name
where column_name operator value
group by column_name;
-- 没有使用聚合函数的列。必须出现在group by 后面
```

```mysql
select count(classname) as '1班' from student where classname = '1班' GROUP BY classname 
```

```mysql
SELECT * FROM student WHERE id IN(select count(1) as '1班' from student GROUP BY classname) 
-- 此时括号里查出的条数可以当数据用
```

```mysql
select classname,age,SUM(age) from student GROUP BY classname,age
-- 按class name分组，当两列数据都相同时，合并为一列
```

查询结果表：

![image-20201023113626743](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201023113626743.png)

student原始表：

![image-20201023113702006](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201023113702006.png)

#### MYSQL 连接的使用

![image-20201023121004427](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201023121004427.png)

![image-20201023121028323](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201023121028323.png)

- ##### INNER JOIN（内连接,或等值连接）：获取两个表中字段匹配关系的记录。（两个表中都有的数据，即交集）

```mysql
select s.name,s.classname,c.course from student s inner join class c on s.classname = c.classname
```

![image-20201023121049469](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201023121049469.png)

- ##### LEFT JOIN（左连接）：获取左表所有记录，即使右表没有对应匹配的记录。（交集加左边表特有的数据）

  ```mysql
  select s.name,s.classname,c.course from student s LEFT JOIN class c on s.classname = c.classname
  ```

  ![image-20201023140655671](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201023140655671.png)

- ##### RIGHT JOIN（右连接）： 与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录。（交集加右边表特有数据）

  ```mysql
  select s.classname from student s RIGHT JOIN class c on s.classname = c.classname
  ```

![image-20201023143453128](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201023143453128.png)

![image-20201023143522632](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201023143522632.png)

#### MYSQL  NULL值处理

##### mysql中处理null 使用 IS NULL和 IS NOT NULL运算符

```mysql
select * from student where height is null
select * from student where height is not null
```

#### MYSQL  事务（transaction）

主要用于处理操作量大，复杂度高的数据。比如在人员管理系统中，你删除一个人员，你需要删除人员的基本资料，也要删除和该人员相关的信息，如信箱，文章等等，这些数据库操作语句就构成一个事务

mysql中只有使用了innodb数据库引擎的数据库或表才支持事务

事务的四个条件

**原子性：**一个事务中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被回滚至事务开始前状态

**一致性：**事物开始之前后结束之后，数据库的完整性没有被破坏

**隔离性：**允许多个并发事务同时对其数据进行读写和修改能力，隔离性可以防止多个事务并发执行时由于交叉而导致数据的不一致，事务隔离分为不同级别：未提交（read  uncommitted），读提交（read committed），可重复读（repeatable read），串行化（serializable）

**持久性：**事务处理结束后，对数据的修改就是永久的

##### 事务控制语句

- **BEGIN** 或 **START TRANSACTION** 显式地开启一个事务；
- **COMMIT** 也可以使用 COMMIT WORK，不过二者是等价的。COMMIT 会提交事务，并使已对数据库进行的所有修改成为永久性的；
- **ROLLBACK** 也可以使用 ROLLBACK WORK，不过二者是等价的。回滚会结束用户的事务，并撤销正在进行的所有未提交的修改；
- **SAVEPOINT identifier**，SAVEPOINT 允许在事务中创建一个保存点，一个事务中可以有多个 SAVEPOINT；
- **RELEASE SAVEPOINT identifier** 删除一个事务的保存点，当没有指定的保存点时，执行该语句会抛出一个异常；
- **ROLLBACK TO identifier** 把事务回滚到标记点；
- **SET TRANSACTION** 用来设置事务的隔离级别。InnoDB 存储引擎提供事务的隔离级别有READ UNCOMMITTED、READ COMMITTED、REPEATABLE READ 和 SERIALIZABLE。

#### mysql事务处理两种方法

##### 1.用begin，rollback,commit来实现

begin 开始一个事务

rollback事务回滚

commit  事务确认

```mysql
begin;
insert into test value(101);
commit  -- 提交
-- 成功插入了一条数据101
```

```mysql
create table test(id int(5))
begin;
insert into test value(9);  -- 插入数据
ROLLBACK   -- 回滚
-- 上述语句因为回滚，所以没有插入数据
```

##### 2.直接用set来改变MYSQL的自动提交模式

set  autocommit = 0禁止自动提交

set  autocommit =1 开启自动提交

#### MYSQL  ALTER 修改表名，字段名

需要修改表名，字段名时，就需要使用此命令

```mysql
-- 删除字段
alter table test drop names
-- 添加字段
alter table test add age varchar(20)
-- 更新字段类型长度
alter table test modify age char(10)
-- 修改字段名称
alter table test change age score tinyint
```

#### MYSQL 处理重复数据

##### 1.防止表中出现重复数据

可设定字段为主键 primary key 或者 unique（唯一）索引来保证数据的唯一性

```mysql
-- 下表无索引无主键，所以该表允许出现多条重复记录
create table test1(
   first_name char(20),
   last_name char(20),
    sex char(10)
);
```



##### 2.统计重复数据

##### 3.过滤重复数据

##### 4.删除重复数据