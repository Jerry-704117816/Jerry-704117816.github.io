---
title: MySQL数据库基本操作
date: 2019-12-30 11:25:00
author: 张晓东
img: 
top: false
cover: false
coverImg: 
toc: false
mathjax: false
summary: MySQL数据库
categories: 数据库
tags:
  - 数据库
---
## MySQL

### 关系型数据库入门

#### 1. 数据持久化

数据库是数据持久化的一种工具， 如果想要做到数据持久化必须将数据通过文件保存到硬盘中。

当我们做数据持久化操作时不仅仅是希望能够把数据长久的保存起来，更为重要的是我们希望很方便的管理数据，在需要数据的时候能够很方便的把需要的数据取出来。数据库比起一般的文件，在数据管理有明显的优势，这也是为什么程序中数据的持久化绝大部分都采用的是数据库

#### 2. 数据库发展史

目前数据库主要分为两种：关系型数据库和NoSQL数据库(在这两个之前还有网状数据库、层次数据库。但是现在都已经不用了)。这儿我们主要介绍第一种数据库，也是就关系型数据库。


1970年，IBM的研究员E.F.Codd在Communication of the ACM上发表了名为A Relational Model of Data for Large Shared Data Banks的论文，提出了关系模型的概念，奠定了关系模型的理论基础。后来Codd又陆续发表多篇文章，论述了范式理论和衡量关系系统的12条标准，用数学理论奠定了关系数据库的基础。


#### 3. 关系型数据库的特点

- 理论基础：集合论和关系代数
- 具体表象：用二维表组织数据

列  — 字段

行  — 记录

- 编程语言：结构化查询语言(SQL)

#### 4.数据库产品排名

- [Oracle](https://www.oracle.com/index.html)    - 目前世界上使用最为广泛的数据库管理系统，作为一个通用的数据库系统，它具有完整的数据管理功能；作为一个关系数据库，它是一个完备关系的产品；作为分布式数据库，它实现了分布式处理的功能。在Oracle最新的12c版本中，还引入了多承租方架构，使用该架构可轻松部署和管理数据库云。

- [MySQL](https://www.mysql.com/)  - MySQL是开放源代码的，任何人都可以在GPL（General Public License）的许可下下载并根据个性化的需要对其进行修改。MySQL因为其速度、可靠性和适应性而备受关注。

- [SQL Server](https://www.microsoft.com/en-us/sql-server/)  - 由Microsoft开发和推广的关系型数据库产品，最初适用于中小企业的数据管理，但是近年来它的应用范围有所扩展，部分大企业甚至是跨国公司也开始基于它来构建自己的数据管理系统。

- [PostgreSQL](https://github.com/jackfrued/Python-100-Days/blob/master/Day36-40) - 在BSD许可证下发行的开放源代码的关系数据库产品。

- [MongoDB](https://docs.mongodb.com)  - MongoDB是2009年问世的一个面向文档的数据库管理系统，由C++语言编写，旨在为Web应用提供可扩展的高性能数据存储解决方案。虽然在划分类别的时候后，MongoDB被认为是NoSQL的产品，但是它更像一个介于关系数据库和非关系数据库之间的产品，在非关系数据库中它功能最丰富，最像关系数据库。 

- [DB2](https://www.ibm.com/analytics/us/en/db2/)  - IBM公司开发的、主要运行于Unix（包括IBM自家的[AIX](https://zh.wikipedia.org/wiki/AIX)）、Linux、以及Windows服务器版等系统的关系数据库产品。DB2历史悠久且被认为是最早使用SQL的数据库产品，它拥有较为强大的商业智能功能。

- [Redis](https://redis.io)  - Redis是一种基于键值对的NoSQL数据库，它提供了对多种数据类型（字符串、哈希、列表、集合、有序集合、位图等）的支持，能够满足很多应用场景的需求。Redis将数据放在内存中，因此读写性能是非常惊人的。

- [ElasticSearch](https://www.elastic.co/cn/)  - ElasticSearch是一个基于[Lucene](https://baike.baidu.com/item/Lucene/6753302)的搜索服务器。它提供了一个分布式多用户能力的全文搜索引擎，基于RESTful web接口。Elasticsearch是用Java语言开发的，并作为Apache许可条款下的开放源码发布，是一种流行的企业级搜索引擎。


### SQL(结构化查询语言)详解

我们通常可以将SQL分为三类：DDL(数据定义语言)、DML(数据操作语言)和DCL(数据控制语言)

- DDL   - 主要负责创建表、删除表和修改表，涉及的指令有: create、drop、alter

- DML  - 主要负责数据的增(insert)、删(delete)、改(update)、查(select)

- DCL  -  通常用于授予权限(grant)和召回权限(revoke)

注意: SQL语句中关键字不区分大小写，并且一条语句结束必须写分号

#### 1. DDL(数据定义语言)

##### 1.1 创建数据库

```mysql
1. create database 数据库名;     -- 创建指定数据库；如果该数据库已经存在会报错
2. create database if not exists 数据库名;      -- 当指定数据库不存在的时候创建数据库；如果存在就不创建，也不会报错
3. create database if not EXISTS 数据库名 default charset utf8;  -- 创建数据库的时候设置字符集编码方式为utf8,让数据库支持中文数据的存储

-- 注意: 可以在通过 character-set-server=utf8 来设置MySQL服务启动时默认使用的字符集

-- 创建school数据库示例：
CREATE DATABASE IF NOT EXISTS school DEFAULT charset utf8;
```



##### 1.2 删除数据库

```mysql
1. drop database 数据库名;     -- 删除指定数据库；如果该数据库不存在会报错
2. DROP DATABASE if EXISTS 数据库名; 	-- 当指定数据库存在的时候删除数据库；如果数据库不存在不会报错

-- 删除school数据库示例:
DROP DATABASE IF EXISTS school;
```



##### 1.3 使用/切换数据库

```mysql
1. use 数据库名;         -- 切换到指定数据库


-- 使用school数据库示例:
USE school;
```



##### 1.4 创建表

```mysql
1. create table if not exists 表名(字段名1 类型1 约束1 comment 描述1, 字段2 类型2 约束2 comment 描述2,...);
-- 1)表名   - 程序员自己命名，但是一般以t或者tb作为前缀表示表名； 而且要见名知义
-- 2)字段名  - 程序员自己命名，要求见名知义
-- 3)类型   - 类型必须是当前数据库支持的类型名，mysql中常见的类型有: int(整数), float(小数),char/varchar/text(字符串)，bit(布尔),date(日期)
-- 4)约束   - 创建约束：not null - 不为空, default  - 设置默认值, unique - 值唯一, primary key - 主键约束 
-- 4.1)主键约束  - 主键的值可以确定列表中唯一一条记录(通过一个主键值可以找到表中的唯一一条记录)，所以一般每张表都需要设置一个字段为主键，主键的值也必须是唯一的；一般需要可以通过auto_increment约束让整型主键自动增加
-- 5)comment    -  添加字段说明

-- 创建学生表示例1:
CREATE TABLE IF NOT EXISTS t_student
(
stuid  int not null PRIMARY KEY auto_increment COMMENT '学号',
stu_name  varchar(20) not null COMMENT '姓名',
stuage  int COMMENT '年龄', 
stugender   bit default 1 COMMENT '性别',
stubirth   date COMMENT '生日'
);

-- 创建教师表示例2:
CREATE TABLE IF NOT EXISTS t_teacher
(
teaid int not null auto_increment COMMENT '编号',
teaname  varchar(20) not null COMMENT '姓名',
teaage int comment '年龄',
teatitle varchar(20) DEFAULT '助教' COMMENT '职称',
PRIMARY KEY (teaid)    -- 主键设置可以在后面单独设置
)
```

##### 1.5 删除表

```mysql
1. DROP TABLE if EXISTS 表名;   -- 删除指定表

-- 删除教师表示例:
DROP TABLE if EXISTS t_teacher;
```



##### 1.6 修改表

###### 1.6.1 添加字段/列

```mysql
1. alter TABLE 表名 add COLUMN 字段名 字段类型 约束 comment 描述;   -- 在指定表中添加指定字段

-- 给学生表添加地址字段示例:
alter TABLE t_student add COLUMN stuaddr varchar(200) DEFAULT '' COMMENT '家庭住址';
```

###### 1.6.2 删除字段/列

```mysql
1. alter TABLE 表名 drop COLUMN 字段名;    -- 删除指定表中的指定字段

-- 示例:
ALTER TABLE t_student DROP COLUMN stuage;
```



#### 2. DML(数据操作语言)

##### 2.1 增(添加记录)

```mysql
1. insert into 表名 values(值1,值2,值3,...)  -- 按照表中字段的顺序依次给每个字段赋值

-- 示例:
insert into t_student values(2,'李四',0,'2017-12-30','成都');


2. insert into 表名(字段1,字段2,字段3,...) values(值1,值2,值3,...);   -- 按指定顺序给指定字段赋值

-- 示例:
insert into t_student(stuname, stugender, stubirth,stuaddr) values('夏明',1,'1992-3-12','大连');

-- 一次插入多条记录  
insert into t_student(stuname, stubirth, stuaddr) values
('小花','1989-10-2','南京'),
('Tom',date(now()),'西安'),
('大黄','2000-1-20','沈阳');


-- 值的问题: sql中是数字对应的值直接写，字符串需要使用引号引起来，bit类型的值只有0或者1, 时间可以用内容是满足时间格式字符串也可以是通过时间函数获取的值
-- 时间函数: now() - 当前时间  date(now()) - 当前日期   year(now()) - 当前年   month(now()) - 当前月 ....
```

##### 2.2 删(删除记录)

```mysql
1. delete from 表名;  -- 删除指定表中所有记录

-- 示例:
delete from t_student;



2. delete from 表名 where 条件语句;    -- 删除满足条件的记录

-- 示例:
delete from t_student where stuid=9;     -- 删除stuid等于9的记录
delete from t_student where stuage=18 and stugender=0;    -- 删除stuage等于18并且stugender等于0的记录
delete from t_student where stuage in (16,17);    -- 删除stuage是16和stuage是17的记录
delete from t_student where stuname like 'stu%';   -- 删除stuname的值是以stu开头的记录
delete from t_student where stuname like '%1';   -- 删除stuname的值是以1结尾的记录
delete from t_student where not age=18;      -- 删除stuage不是18的记录
delete from t_student where birth is NULL;   -- 删除stubirth是NULL的记录

-- 条件语句的写法
-- 1)比较运算符: =(等于), <>(不等于),>(大于), <(小于),>=(大于等于), <=(小于等于)
-- 2)逻辑运算符: and(并且), or(或者), not(非)
-- 3)是否为空: is null(为空), is not null(不为空)
-- 4)范围: between x and y(在x到y之间), not between x and y(不在x到y之间)
-- 5)字符串匹配: like 字符串（像, like后面的字符串可以使用%表示任意个任意字符, _表示任意一个字符）
-- 6)指定集合元素: in (值1,值2,...)(结果是集合中的元素)
```

##### 2.3 改(修改数据/记录) 

```mysql
1. update 表名 set 字段1=新值1, 字段2=新值2,...;  	-- 将指定表中所有行的指定列/字段的值赋值为新值

-- 示例:
update t_student set stubirth='1992-3-12';     -- 将所有记录中的stubirth字段都设置为1992-3-12




2. update 表名 set 字段1=新值1, 字段2=新值2,... where 条件语句;  -- 将表中满足条件的行中指定字段的值赋值为新值 

-- 示例:
update t_student set stuage=20 where not stuname like 'stu%';  -- 将所有stuname不是stu开头的记录的stuage字段设置为20
```



##### 2.4 查(获取数据)

###### 2.4.1 直接查询

```mysql
1. select * from 表名;    -- 获取指定表中所有行和所有的列(所有数据)

-- 示例:
SELECT * FROM t_student;


-- 映射
2. select 字段名1,字段名2,... from 表名;   -- 获取指定表中所有行指定的列

-- 示例:
SELECT stuname,stuid FROM t_student; 



3. select * from 表名 where 条件;    -- 获取指定表中所有满足条件的行所有列的数据

-- 示例:
SELECT * FROM t_student WHERE stuid>115; 
SELECT stuname,stuage FROM t_student WHERE stuid>115;
```

###### 2.4.2 列重命名

```mysql
1. select 字段1 as 新字段1, 字段2 as 新字段2,... from 表名; 
-- 注意： 这儿的as可以省略

-- 示例：
select stuname as '姓名', stuage as '年龄' from t_student;
```



###### 2.4.3 对查询结果重新赋值(一般针对布尔数据)

```mysql
1. select if(字段名,值1,值2) from 表名;    -- 查询指定字段，并且判断字段对应的值是0还是1，如果是1结果为值1，否则为值2
-- 注意: 这儿的if的用法是MySQL专有的
-- MySQL写法: if(字段, 新值1, 新值2)
-- 通用写法: case 字段 when 值 then 新值1 else 新值2 end

-- 示例:
select stuname, if(stugender, '男', '女') from t_student;   -- 查询的时候如果stugender的结果不再是0或者1而是男或者女
select stuname, case stugender when 1 then '男' else '女' end from t_student; -- 查询的时候如果stugender的结果不再是0或者1而是男或者女
```



###### 2.4.4 对列进行合并

```mysql
1. select concat(字段1,字段2,...) from 表名;  

-- 示例:
select concat(stuname, stuage) from t_student;    -- 将多个字段的数据合并成一个数据返回
select concat(stuname, stuage) as 'nameage' from t_student;    -- 将多个字段的数据合并成一个数据返回并且为其数据重命名
select concat(stuname, ':', stuid) as 'name_id' from t_student;  

-- 注意: 数字和字符串数据可以合并，bit类型的数据不可以合并
```



###### 2.4.5 模糊查询 - 查询的时候时候通过like条件来指定查询对象

```mysql
-- 示例:
select * from t_student where stu_name like 'stu%' and gender=0;
```



###### 2.4.6 排序(先按之前的任何语法进行查询在排序)

```mysql
1. select * from 表名 order by 字段;      -- 对查询结果按照指定字段的值进行升序排序 
2. select * from 表名 order by 字段 asc;      -- 对查询结果按照指定字段的值进行升序排序 
3. select * from 表名 order by 字段 desc;      -- 对查询结果按照指定字段的值进行降序排序

-- 示例:
select * from t_student order by stuage;
select * from t_student order by stuage asc;
select * from t_student order by stuage desc;
select * from t_student order by age asc, gender asc;  -- 对查询结果先按年龄进行排序；年龄相同的再按性别进行排序
```



###### 2.4.7 去重

```mysql
1. select distinct 字段 from 表名;   -- 获取指定字段的值并且去重

-- 示例:
select distinct stuage from t_student;
```



###### 2.4.8 限制和分页

```mysql
1. select * from 表名 limit 数量;  -- 值获取指定数量的查询结果

-- 示例:
select * from t_student limit 3;    -- 获取查询结果的前3条



2. select * from 表名 limit M offset N;   -- 跳过前N条数据获取M条数据

-- 示例:
select * from t_student limit 3 offset 4;   -- 跳过前4条数据获取3条数据



3. select * from 表名 limit M,N;   -- 跳过前M条数据获取N条数据

-- 示例:
select * from t_student limit 3,4;    --  跳过前3条数据获取4条数据
```



#### 3. 外键与E.R图

##### 3.1 约束管理

###### 3.1.1 添加约束

 添加普通约束的方式有两种，一种是创建表的时候直接给字段添加相应的约束，另一种是通过修改表的方式添加约束

```mysql
1. 创建表的时候添加约束
建表的时候可以在字段类型后面加一个或者多个约束

2.通过添加约束索引的方式添加约束
alter table 表名 add constraint 索引名 约束(字段);
-- 说明: 索引名 - 自己随便命名;  约束 - 当前想要添加的约束(但是只支持唯一约束、主键约束和外键约束)

-- 示例:
alter table t_teacher add constraint uni_tel UNIQUE(teatel);                      
```



###### 3.1.2 删除约束

```mysql
alter table 表名 drop index 约束索引;

-- 示例:
alter table t_teacher drop index uni_tel;
```



##### 3.2 外键约束

```mysql
1.什么是外键：表中的某个字段的值是根据其他表中主键的值来确定的。那么这个字段就是外键 
1.1 不同类型的外键添加方法：
	多对一的外键的添加： 将外键添加到多的一方对应的表中 
	一对一的外键的添加： 将外键随便添加到哪一方，同时添加值唯一约束
	多对多的外键的添加： 关系型数据库中，两张表没法实现多多的关系，需要一个中间表。(中间表有两个外键分别参照		               多多的两个表的主键)
1.2 添加外键约束语法:
	alter table 表名1 add constraint 外键约束索引名 foreign key (字段1) references 表名2 (字段2);
	-- 将表1中的字段1设置为外键，并且让这个外键的值参照表2中的字段2
	
1.3 删除外键约束
	alter table 表名 drop foreign key 外键索引名;
```



##### 3.3 高级查询

###### 3.3.1  聚合：max()/min()/sum()/avg()/count()

```mysql
SELECT score FROM tb_score;
SELECT max(score) as max_score FROM tb_score;   -- 获取tb_score表中字段score的最大值
SELECT min(score) as min_score FROM tb_score;   -- 获取tb_score表中字段score的最小值
SELECT sum(score) as sum_score FROM tb_score;   -- 获取tb_score表中字段score的和
SELECT AVG(score) as avg_score FROM tb_score;   -- 获取tb_score表中字段score的平均值
SELECT COUNT(score) as count_score FROM tb_score WHERE score>80;  -- 统计tb_score表中字段score大于80的个数
```

###### 3.3.2  分组

```mysql
SELECT 字段操作  FROM 表名 WHERE 条件 GROUP BY(字段2);
-- 将指定表中满足条件的记录按照字段2的进行分组(值是一样的在一个组里面), 然后再讲每个分组作为整体按照指定字段进行指定聚合操作
-- 注意:a.字段操作的位置除了分组字段不用聚合，其他字段都必须聚合   b.分组的时候where要放到分组前对需要分组的数据进行筛选

select stuid, avg(score) from tb_score group by(stuid);

-- having: 分组的时候，在分组后用having代替where来对分组后的数据进行筛选
select stuid, max(score) from tb_score group by(stuid) having max(score)>90;
select stuid, avg(score) from tb_score group by(stuid) having avg(score)>80;
```



###### 3.3.3 子查询

```mysql
-- 将一个查询的结果作为另外一个查询的条件或者查询对象
-- 第一种子查询: 将查询结果作为另外一个查询的条件

-- 获取成绩大于90分的学生姓名
select stuname from tb_student where stuid in 
(select stuid from tb_score where score>90);

-- 第二周子查询：将一个查询的结果作为查询对象提供给另外一个查询。但是第一个查询结果需要重命名 
select score from (SELECT stuid,score from tb_score where score>80) as t2;
```



###### 3.3.4 连接查询 - 同时查询多张表

```mysql
1. 直接连接
select * from 表名1,表名2,表名3 连接条件 查询条件;
-- 注意: 如果既有连接条件又有查询条件，查询条件必须放在连接条件的后面

-- 查询所有学生的名字和学院名字
select stuname, collname from tb_student, tb_college where tb_student.colid=tb_college.collid;

2.内连接
SELECT * FROM 表1 inner join 表2 on 表2的连接条件 inner join 表3 on 表3的连接条件 ...;
-- 注意: 中间表写在最前面(存在关联其他表外键的表)

3.外连接
-- 外连接分为左外连接、右外连接和全连接， 但是在MySQL中支持左外连接和右外连接 
-- 左外连接：将左表中对应字段的所有数据取出，然后再对应的右表中字段的值，如果右表对应的值不存在结果就为null 
-- 右外连接：将右表中对应字段的所有数据取出，然后再对应的左表中字段的值，如果左表对应的值不存在结果就为null 
select * from 表1 left join 表2 on 连接条件;
select * from 表1 right join 表2 on 连接条件;

-- 获取所有学生的成绩
select stuname, score from tb_student left join tb_score on tb_student.stuid=tb_score.sid;
```



#### 4. DCL(数据控制语言)

DCL主要提供grant和revoke来授权和召回权限

##### 4.1 用户管理

```mysql
1. 添加用户
create user 用户名@登录地址;    -- 创建数据用户，登录不需要密码
-- 登录地址 - 限制用户能够登录MySQL的主机地址，可以赋值为: ip地址(指定地址)、localhost(数据库本机)、%(任何位置)
create user 用户名@登录地址 identified by 密码; -- 创建数据用户，登录需要输入指定密码密码

-- 示例:
create user zhangsan@localhost;
create user lisi@localhost identified by '123456';

2. 删除用户
drop user 用户名;
drop user zhangsan;
```

##### 4.2 权限管理

```mysql
1. 授权
grant 权限类型 on 数据库.对象 from 用户名;
-- 常见权限类型: delete(删除权限), select(查询权限),update(更新权限),insert(插入权限), all PRIVILEGES(所有权限)

-- 示例:
GRANT SELECT on school.tb_student TO 'zhangshan';
GRANT UPDATE on school.tb_student TO 'zhangshan';
GRANT all PRIVILEGES ON school.* TO 'zhangshan';   -- 添加所有权限


2.召回授权
revoke 权限类型 on 数据库.对象 from 用户名;

-- 示例:
REVOKE DELETE on school.* FROM 'zhangshan';
REVOKE all PRIVILEGES on school.* FROM 'zhangshan';
REVOKE all PRIVILEGES on school.* FROM 'zhangshan';
REVOKE SELECT on school.tb_student FROM 'zhangshan';
REVOKE UPDATE on school.tb_student FROM 'zhangshan';
```

##### 4.3 事务

完成一个任务需要执行多条sql，但是要求这多个操作中只要有一个操作失败，这个任务就失败，数据全部还原；所有的操作都成功，整个任务才成功的时候就使用事务

```mysql
-- 开启事务环境
begin;
需要执行的多个操作对应的sql语句

-- 提交事务(只有begin到commit之间的所有的sql都执行成功，才会执行commit; 否则执行rollback)
COMMIT;
-- 事务回滚(放弃beigin到commit之间执行成功的所有sql语句的结果)
ROLLBACK;
```



#### 5. 视图

视图是关系型数据库中将一组查询指令构成的结果集组合成可查询的数据表的对象。简单的说，视图就是虚拟的表，但与数据表不同的是，数据表是一种实体结构，而视图是一种虚拟结构，你也可以将视图理解为保存在数据库中被赋予名字的SQL语句。

使用视图可以获得以下好处：

1. 可以将实体数据表隐藏起来，让外部程序无法得知实际的数据结构，让访问者可以使用表的组成部分而不是整个表，降低数据库被攻击的风险。
2. 在大多数的情况下视图是只读的（更新视图的操作通常都有诸多的限制），外部程序无法直接透过视图修改数据。
3. 重用SQL语句，将高度复杂的查询包装在视图表中，直接访问该视图即可取出需要的数据；也可以将视图视为数据表进行连接查询。
4. 视图可以返回与实体数据表不同格式的数据，

```mysql
1. 创建视图
create view 视图名 as sql查询语句;

-- 示例:
create view vw_student
as SELECT * FROM tb_student;



2. 使用视图  - 视图在用的时候可以直接当成表来使用

-- 示例:
select * FROM vw_student;

select stuname, collname from vw_student, tb_college where vw_student.colid=tb_college.collid;
```



#### 6. 索引

索引相当于书本的目录，为表创建索引可以加速查询（用空间换时间）。

索引虽然很好，但是不能滥用：

- 索引会占用额外的空间

- 索引会让增删改变得更慢

如果哪个列经常被用于查询的筛选条件那么就应该在这个列上建立索引。

主键上有默认索引(唯一索引)

```mysql
1. 创建索引
-- 如果使用模糊查询，查询条件不以%开头，那么索引有效
-- 如果使用模糊查询，查询条件以%开头，那么索引无效(尽量避免)
create index 索引名 on 表名 (字段);    -- 给指定表的指定字段添加索引
create unique index 索引名 on 表名 (字段);  -- 给指定表的指定字段添加唯一索引

-- 示例:
create index idx_stuname on tb_student(stuname);
create unique index idx_stuname on tb_student(stuname);


2. 删除索引
alter table 表名 drop index 索引名; 		-- 删除指定索引，唯一索引也是这样删

-- 示例: 
alter table tb_student drop index idx_stuname;


注意: 可以通过explain来查看sql的执行计划
```

























