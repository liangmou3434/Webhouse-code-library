1. 数据库的概念
2. 下载并配置MySQL
3. MYSQL数据模型
4. SQL简介
5. 综合案例
# 1.数据库的概念
==数据库==:DataBase(DB),是村粗和管理数据的仓库
==数据库管理系统==:DataBase Management System(DBMS),操纵和管理数据库的大型软件
==SQL==:Structured Query Language(结构化查询语言),操作关系型数据库的变成语言,定义了一套操作关系型数据库的统一标准


# 2.下载并配置MySQL
MySQL的官网:[MySQL :: Download MySQL Community Server](https://dev.mysql.com/downloads/mysql/)
1) 下载安装包并解压
2) 配置环境变量
![[Pasted image 20250227215121.png]]
3) 检验环境变量是否配置成功
_在命令行中输入`mysql`_
出现下面错误信息为配置成功
![[Pasted image 20250227215307.png]]

## 2.1初始化MySQL的数据
在管理员身份的命令行中输入
```
mysqld --initialize-insecure
```
![[Pasted image 20250227215923.png]]

## 2.2注册MYSQL服务
_在管理员身份的命令行中执行下面的指令_
```
mysqld -install
```
![[Pasted image 20250228084804.png]]
![[Pasted image 20250228085040.png]]
**MYSQL成功注册成系统服务并在开机时自动启动**

## 2.3启动MYSQL服务
_在命令行下输入下面的指令,分别为启动MYSQL服务和停止MYSQL服务_
```
net start mysql  // 启动mysql服务
net stop mysql  // 停止mysql服务
```
![[Pasted image 20250228091423.png]]

## 2.4修改账户默认密码
```
mysqladmin -u root password 1234
```
1234为修改后的密码-可以任意修改自己喜欢的(我的密码与校园圈密码相同)


## 2.5登录MYSQL
```
mysql -uroot -p1234(1234部分修改成自己的密码)//登录
exit//退出
或
quit//退出
```
**-u+用户名 -p+密码**

_使用更安全的方法登录MYSQL
先输入_
```
mysql -uroot -p
```
再输入**密码**
![[Pasted image 20250228092507.png]]

## 2.6卸载MYSQL
以管理员身份执行命令行,输入
```
net stop mysql+回车
mysqld -remove mysql+回车
```
**最后删除相关的目录及环境变量**
语法
```
mysql -u用户名 -p密码[-h数据库服务器IP地址(不指定时为0.0.1) -p端口号(不指定端口号时使用默认端口号3306)]
```

# 3.MYSQL数据模型
*  关系型数据库(RDBMS):建立在关系模型的基础上,由多张相互连接的==二维表==组成的数据库

## 3.1连接数据库
创建一个新的数据库
登录后使用命令
```
CREATE DATABASE 数据库名字;
```
![[Pasted image 20250228112819.png]]
**一个数据库服务器中可以创建多个数据库,而且数据库之间是相互独立,互不影响的**

# 4.SQL简介
==SQL==:一门操作关系型数据库的编程语言,定义操作所有关系型数据库的统一标准

## 4.1SQL的通用语法
1) SQL语句可以单行或多行书写,以分号结尾
2) SQL语句可以使用空格/缩进来增强语句的可读性
3) MSQL数据库的SQL语句不区分大小写
4) 注释
1. 单行注释:`--`注释内容或`#`注释内容(MYSQL特有)
2. 多行注释:`/*注释内容*/`

## 4.2SQL语句的分类
1) ==DDL==:(Data Definition Language)-数据定义语言,用来定义数据库对象(数据库,表,字段)
2) ==DML==:(Data manipulation Language)-数据操作语言,用来对数据库中的数据进行增删改
3) ==DQL==:(Data Query Language)-数据查询语言,用来查询数据库中表的记录
4) ==DCL==:(Data Control Language)-数据控制语言,用来创建数据库用户,控制数据库的访问权限

## 4.3DDL语句
==DDL==:(Data Definition Language)-数据定义语言,用来定义数据库对象(数据库,表,字段)

### 4.3.1数据库
1) ==查询==
*  查询所有数据库
```
show databases;
```
* 查询当前数据库
```
select databases();
```

2) ==使用==
* 使用数据库
```
use 数据库名;
```

3) ==创建==
* 创建数据库
```
create database[if not exists] 数据库名;
```

4) ==删除==
 * 删除数据库
```
drop database[if exists] 数据库名;
```

==注意:==**上述语法中的database也可以替换成schema**
### 4.3.2表(创建,查询,修改,删除)
1) 表结构的创建
语法:
```
creat table 表名(
      字段1 字段类型[约束][comment 字段1注释],
      ......
      字段n 字段类型[约束][comme nt 字段n注释]
)[comment 表注释];
```
==注意:==语法中`[]`的内容是可选的,可以加也可以不加
例:创建下图表结构
![[Pasted image 20250303115039.png]]
```
create table tb_user(  
    id int comment 'ID,唯一标识',  
    username varchar(20) comment'用户名',  
    name varchar(10) comment'姓名',  
    age int comment '年龄',  
    gender char(1) comment'性别'  
)comment '用户表';  
-- varchar相当于java中的字符串类型 varchar(20)表示该字符串长度最长为20\  
-- comment后面为字段的注释
```
![[Pasted image 20250303115306.png]]

2) 表结构的查询
* 查询当前数据库的所有表
```
show tables;
```
* 查询表结构
```
desc 表名;
```
* 查询建表语句
```
show create table 表名;
```

3) 修改表结构
```
-- 添加字段
alter table 表名 add 字段名 类型(长度)[comment 注释][约束]
-- 修改字段类型
alter table 表名 modify 旧字段名 新字段名 类型(长度)[comment 注释][约束]
-- 修改字段名和字段类型
alter table 表名 change 旧字段名 新字段名 类型(长度)[comment 注释][约束]
-- 删除字段
alter table表名 drop column字段名
-- 修改表名
rename table 表名 to 新表名
```

4) 删除表结构
```
drop table[if eists]表名;
```


### 4.3.3对数据库中约束的详细说明
概念:约束是作用于表中字段上的规则,用于限制存储在表中的数据
目的:保证数据库中数据的正确性,有效性和完整性
1) 非空约束:限制字段值不能为空,`not null`
2) 唯一约束:保证字段的所有数据都是唯一的,不重复的,`unique`
3) 主键约束:主键是一行数据的唯一标识,要求非空且唯一,`primary key`(auto_increment自增)
==auto_increment==:自动从1往上增长
4) 默认约束:保存数据时,如果未指定该字段值,则采用默认值,`default`(default要加默认值)
5) 外键约束:让两张表的数据建立连接,保证数据的一致性和完整性,`foreign key`

例:在创建的数据库表示中添加约束
![[Pasted image 20250303161559.png]]
```
-- 创建:基本语法(约束)  
create table tb_user(  
    id int unique auto_increment comment'ID,唯一标识',  
    username varchar(20) primary key comment '用户名',  
    name varchar(10) not null comment'姓名',  
    age int comment '年龄',  
    gender char(1) default'男' comment'性别'  
)comment '用户表';
```

### 4.3.4DDL语句中的数据类型
MySQL中的数据类型有很多,主要分为三类:数值类型,字符串类型,日期时间类型
1) 数值类型
**以tinyint为例,如果仅使用tinyint作为数据类型则默认为有符号范围,使用无符号范围需要用`tinyint unsigned`**
![[Pasted image 20250303162156.png]]
2) 字符串类型
**char(10)**:最多只能存10个字符,不足时10个字符,也会占用10个字符的空间,
**varchar(10)**:最多只能存10个字符,不足10个字符时,按照实际长度进行空间占用
==char不需要判断字符存储的空间,相较于varchar来说性能较高,而varchar需要判断字符空间,相较与char性能较低==
![[Pasted image 20250303162254.png]]
3) 日期时间类型
![[Pasted image 20250303162315.png]]
## 4.4使用IDEA连接数据库
**在IDEA中创建一个空项目**
![[Pasted image 20250303105325.png]]
![[Pasted image 20250303112318.png]]

## 4.4.1在IDEA中对数据库进行操作
**除使用SQL语句对数据库进行增删改查外的方法对数据库进行管理**
![[Pasted image 20250303113143.png]]

**快速找到consel控制台界面**
![[Pasted image 20250303113635.png]]

**在创建的表格中添加数据**
![[Pasted image 20250303153959.png]]

## 4.5DML语句
==DML:==DML的英文全称是Data Manipulate Language(数据操作语言),用于对数据库中表的记录进行增删改操作
### 4.5.1添加数据(INSERT)
* ==指定字段添加数据==:insert into 表名(字段名1,字段名2) values(值1,值2)
* ==全部字段添加数据==:insert into 表名 values(值1,值2...)
* ==批量添加数据(指定字段)==:insert into 表名(字段名1,字段名2) values(值1,值2)(值1,值2)
* ==批量添加数据(全部字段)==:insert into 表名 values(值1,值2...)(值1,值2...)
```
-- DML:数据操作语言  
-- DML:插入数据:insert  
-- 1.为tb_staff表中的username,name,gender字段插入值  
-- 使用now()函数把当前时间赋值给创建时间和更新时间  
insert into tb_staff(username,name,gender,create_time,` update_time`)  
values ('liangmou2121','梁某',1,now(),now());  
  
-- 2.为tb_staff表中的所有字段插入值  
insert into  tb_staff  
      values(null,'limou3434','123','李某',1,'1.jpg',2,'2004-09-23',now(),now());  
  
-- 3.批量为tb_staff表中的username,name,gender字段插入数据  
insert into tb_staff(username,name,gender,create_time,` update_time`)  
values ('zhangsan','张三',1,now(),now()),('lisi','李四',2,now(),now());
```
==注意:==
**1)插入数据时,指定的字段顺序需要与值的顺序是一一对应的
2)字符串和日期型数据应该包含在引导中
3)插入的数据大小,应该在字段的规定范围内**
### 4.5.2修改数据(UPDATE)
* ==修改数据==:update 表名 set 字段名1=值1,字段名2=值2,...`[where 条件]`
```
-- DML:更新数据  
-- 1.将tb_staff表中id为1员工的姓名name字段更新为张三  
-- 更新时间也需要修改  
update tb_staff set name ='张三' ,` update_time` = now() where id = 1;  
  
-- 2.将tb_staff表的所有员工的入职日期更新为'2010-01-01'  
update tb_staff set entrydate = '2010-01-01',` update_time` = now();
```
==注意==:修改语句的条件可以有,也可以没有,如果没有条件,则会修改整张表的数据
### 4.5.3 删除数据(DELETE)
* ==删除数据==:delete from 表名`[where 条件]`
```
-- DML:删除数据-delete  
-- 1.删除tb_staff表中id为1的员工  
delete from tb_staff where id = 1;  
  
-- 2.删除tb_staff表中的所有员工  
delete from tb_staff;
```
==注意==:1)DELETE语句的条件可以有,也可以没有,如果没有条件,则会删除整张表的所有数据
    2)DELETE语句不能删除某一个字段的值,如果要操作可以使用UPDATE,将该字段的值置为NULL



## 4.6DQL语句
==DQL==:DQL英文全称是Data Query Language(数据查询语言),用来查询数据库表中的记录
==关键字==:SELETE

### 4.6.1DQL语法
1) 基本查询
* ==select==:字段列表
* ==from==:表名列表
2) 条件查询
* ==where==:条件列表
3) 分组查询
* ==group by==:分组字段列表
* ==having==:分组后条件列表
4) 排序查询
* ==order by==:排序字段列表
5) 分页查询
* ==limit==:分页参数

### 4.6.2基本查询
**基本查询的语法**:
* ==查询多个字段==:select 字段1,字段2,字段3 from 表名;
* ==查询所有字段(通配符)==:select * from 表名;
* ==设置别名==:select 字段1`[as 别名1]`,字段2`[as 别名2]` from 表名;
* ==去除重复记录==:select distinct 字段列表 from 表名;
```
-- DQL:基本查询  
-- 1.查询指定字段 name,entrydate 并返回  
select name,entrydate from tb_emp;  
  
-- 2.查询并返回所有字段  
-- 1)第一种方式-推荐  
select id, username, password, name, gender, image, job, entrydate, create_time, update_time from tb_emp;  
-- 第二种方式-不推荐(不直观,性能低)  
select * from tb_emp;  
  
-- 3.查询所有员工name,entrydate,并起别名(姓名,入职日期)  
# select name as 姓名,entrydate as 入职日期 from tb_emp;-- 省略as  
-- 如果别名中有特殊符号如空格或下划线,需要对别名添加上单引号或者双引号  
-- 例;select name '姓 名',entrydate '入职_日期' from tb_emp;  
  
-- 4.查询已有员工关联了哪几种职位(不要重复)  
select distinct job from tb_emp;
```
==注意==:1)`*`代表所有字段,在实际开发中尽量少用(不直观,影响效率)
     2)as关键字可以省略

### 4.6.3条件查询
**条件查询的语法:**
* ==条件查询==:select 字段列表 from 表名 where 条件列表;
**比较运算符**
1) `>`-大于
2) `>=`-大于等于
3) `>`-小于
4) `<=`-小于等于
5) `=`-等于
6) `<>`或者`!=`-不等于
7) `between...and`-在某个范围之内(含最小,最大值)
8) `in(...)`-在in之后的列表中的值,多选一
9) `like 占位符`-模糊匹配(_匹配单个字符,%匹配任意个字符)
10) `is null`-是null
11) `and或&&`-并且(多个条件同时成立)
12) `or或||`-或者(多个条件任意一个成立)
13) `not或!`-非,不是
```
-- 分组查询  
-- 1.查询姓名为杨逍的员工 where后面写要查询的条件-从数据库的所有表中查询姓名为杨逍的信息  
select * from tb_emp where name = '杨逍';  
  
-- 2.查询id小于等于5的员工信息  
select * from tb_emp where id <= 5;  
  
-- 3.查询没有分配职位的员工信息-查询job为null的员工  
select * from tb_emp where job is null;  
  
-- 4.查询有职位的员工信息  
select * from tb_emp where job is not null;  
  
-- 5.查询密码不等于'123456'的员工信息  
select * from tb_emp where password != '123456';  
-- 或  
select * from tb_emp where password <> '123456';  
-- 6.查询入职日期在'2000-01-01(包含)到'2010-01-01'(包含)之间的员工信息  
select * from tb_emp where entrydate >='2000-01-01' and entrydate <='2010-01-01';  
-- 或  
select * from tb_emp where entrydate between'2000-01-01' and '2010-01-01';  
-- 7.查询入职日期在'2000-01-01(包含)到'2010-01-01'(包含)之间且性别为女的员工信息  
select  * from tb_emp where entrydate between '2000-01-01' and '2010-01-01' and gender = 2;  
-- 或  
select  * from tb_emp where entrydate between '2000-01-01' and '2010-01-01' && gender = 2;  
-- 8.查询职位是2(讲师),3(学生主管),4(教研主任)的员工信息  
select  * from tb_emp where job = 2 or job = 3 or job = 4;  
-- 或  
select  * from tb_emp where job = 2 || job = 3 || job = 4;  
-- 或  
select * from tb_emp where job in(2,3,4);  
-- 9查询姓名为两个字的员工信息  
select * from tb_emp where name like'__';  
  
-- 10.查询姓'张'的员工信息  
select * from tb_emp where name like'张%';
```
### 4.6.4分组查询
==聚合函数==:将一列数据作为一个整体,进行纵向计算
**语法1**:select 聚合函数(字段列表) from 表名;
1) count:统计数量
2) max:最大值
3) min:最小值
4) avg:平均值
5) sum:求和
```
-- DQL:分组查询  
-- 聚合函数-不对null值进行计算  
-- 1.统计该企业员工数量  
-- A.count(字段)-使用字段统计时,要选择非空字段  
select count(id) from tb_emp;  
-- B.count(常量)  
select count(1) from tb_emp;  
-- C.count(*)-统计表的总数据量-推荐使用  
select count(*) from tb_emp;  
  
-- 2.统计该企业最早入职的员工-最早(小)的入职日期-min  
select min(entrydate) from tb_emp;  
  
-- 3.统计该企业最迟入职的员工-最晚(大)的入职日期-min  
select max(entrydate) from tb_emp;  
  
-- 4.统计该企业员工ID的平均值-avg  
select  avg(id) from tb_emp;  
  
-- 5.统计该企业员工的ID之和-sum  
select  sum(id) from tb_emp;
```
==注意==:
* null值不参与所有聚合函数运算
* 统计数量可以使用:count(`*`),count(字段),count(常量),推荐使用count(`*`)

**语法2**:==分组查询== select 字段列表 from 表名`[where 条件]` group by 分组字段名 `[having 分组后过滤条件]`
```
- 分组  
-- 1.根据性别分组,统计男性和女性员工的数量  
-- select后返回的结果有两类,一类是分组字段,一类是聚合函数  
select gender,count(*) from tb_emp group by gender;  
  
-- 2.先查询入职时间在'2015-01-01'(包含)以前的员工,并对结果根据职位分组,获取员工数量大于等于2的职位  
select job,count(*) from tb_emp where entrydate <= '2015-01-01' group by job having count(*) >= 2;  
-- 先使用where条件进行约束-入职时间在2015-01-01(包括)以前  
-- select * from tb_emp where entrydate <= '2015-01-01' ;  
-- 再根据职位进行分组,返回聚合函数和分组字段-count聚合函数用于统计数量  
select job,count(*) from tb_emp where entrydate <= '2015-01-01' group by job;  
-- 最后只呈现员工数量大于等于2的职位  
-- select job,count(*) from tb_emp where entrydate <= '2015-01-01' group by job having count(*) >= 2;
```
==注意==:where和having的区别
1) 执行时机不同:where是分组之前进行过滤,不满足where条件,不参与分组,而having是分组之后对结果进行过滤
2) 判断条件不同,where不能对聚合函数进行判断,而having可以
3) 分组之后,查询的字段一般为聚合函数和分组字段,查询其他字段无任何意义
4) 执行顺序:where>聚合函数>having

### 4.6.5排序查询
==条件查询==:select 字段列表 from 表名`[where 条件列表]``[group by 分组字段]`order by 字段1 排序方式1,字段2,排序方式2...;
**排序方式**:
* ASC:升序(默认值)
* DESC:降序
```
-- 排序查询  
-- 1.根据入职时间,对员工进行升序排序-asc  
-- 如果需要升序排序,可以省略asc 在系统中排序是默认为升序的  
# select * from tb_emp order by entrydate asc;  
select * from tb_emp order by entrydate;  
  
-- 2.根据入职时间,对员工进行降序排序-desc  
select * from tb_emp order by entrydate desc;  
  
-- 3.根据入职时间对公司的员工进行升序排序,入职时间相同,再按照更新时间进行升序排序  
select * from tb_emp order by entrydate desc,update_time desc;
```
==注意==:如果是多字段排序,当第一个字段值相同时,才会根据第二个字段进行排序

### 4.6.6分页查询
==分页查询==:select 字段列表 from 表名 limit 起始索引,查询记录数;
**起始索引**:从哪一条记录往后进行查询(从0开始)
**起始索引 = (页码 - 1) `*` 每页展示的记录数**
**查询记录数**:每一页需要展示多少条数据
```
-- 分页查询  
-- 1.从起始索引0开始查询员工数量,每页展示五条记录  
select * from tb_emp limit 0 , 5 ;  
  
-- 2.查询第1页员工数据,每页展示5条记录  
select * from tb_emp limit 0 , 5 ;  
  
-- 3.查询第2页员工数据,每页展示5条记录  
select * from tb_emp limit 5 , 5 ;  
  
-- 4.查询第3页员工数据,每页展示五条记录  
select * from tb_emp limit 10 , 5 ;
```
==注意:==
* 起始索引从0开始,起始索引=(查询页码-1)`*`每页显示记录数
* 分页查询时数据库的方言,不同的数据库有不同的实现,在MySQL中是LIMIT
* 如果查询的是第一页的数据,起始索引可以省略,直接简写为limit 查询记录数
例: 查询第一页的五条记录  
```
select * from tb_emp limit 5;
```

# 5.综合案例
## 5.1案例
1) 案例1:
```
-- 案例1:按需求完成员工管理系统分页查询-根据输入条件,查询第一页数据,每页展示10条记录  
-- 输入条件:  
-- 姓名:张  
-- 性别:男  
-- 入职时间:2000-01-01到2015-12-31  
-- 对最后查询的结果根据修改时间进行倒序排序  
-- 对语句进行格式化代码 ctrl + alt + lselect *  
from tb_emp  
where entrydate between '2000-01-01' and '2015-12-31' && name like '%张%' && gender = 1  
order by update_time desc  
limit 0,10;
```

2) 案例2:
```
-- 案例2-1:根据需求,完成员工性别信息的统计count(*)  
-- 统计男性员工和女性员工分别有多少人  
-- 使用if表达式将性别从1,2转换成真实值  
-- if(条件表达式,true取值,false取值)  
# select gender,count(*) from tb_emp group by gender;  
select if(gender = 1,'男性员工','女性员工')性别,count(*) from tb_emp group by gender;
```

## 5.2if条件表达式
==if条件表达式的语法==:if(条件表达式,true取值,false取值)`[别名]`
![[Pasted image 20250308204522.png]]

## 5.3case表达式
==case表达式语法==:case表达式 when 值1 then 结果1 when 值2 结果2...else...end
**case语法用于有多种情况需要从数字转换成具体值**
```
-- 案例2-2:根据需求,完成员工职位信息的统计  
-- 使用case语法表达式 case表达式 when 值1 then 结果1 when 值2 then 结果2...else...end  
-- 下列sql语句中job为表达式  
select  
    (case job when 1 then '班主任' when 2 then '讲师'  
    when 3 then'学生主管' when 4 then '教研主管'  
    else '未分配职位' end)职位, count(*)  
from tb_emp  
group by job;
```
