1. 多表的概念
2. 多表查询
3. 事务
4. 索引

# 1.多表的概念
**在项目开发中,在进行数据库表结构设计时,会根据业务需求以及业务模块之间的关系,分析并设计表结构,由于业务之间相互关联,所以各个表结构之间也存在着各种练习,基本上分为三种**
* 一对多(多对一)
* 多对多
* 一对一

## 1.1一对多
**在一对多中,一也叫`子`表,多也叫`父表`,以员工及部门为例,一个员工只能对应一个部门,一个部门可以对应多个员工,所以员工表也叫做`子表`,部门表也叫做`父表`**
==一对多关系实现:==在数据库表中多的一方,添加字段,来关联一是一方的主键

### 1.1.1外键约束
==概念==:使用foreign key定义外键关联的另一张表
==缺点:==(物理外键)
* 影响增,删,改的效率(需要检查外键关系)
* 仅用于单节点数据库,不适用与分布式,集群场景
* 容易引发数据库的死锁问题,消耗性能
* 为了解决上述问题,在开发中多使用逻辑外键
==外键语法:==
```
-- 创建表时指定
create table表名(
       字段名 数据类型
       ...
       [constraint][外键名称] foreign key(外键字段名) reference 主表(字段名)
);
-- 建完表后,添加外键
alter table 表名 add constraint 外键名称 foreign key(外键字段名) reference 主表(字段名)
```

**添加外键**
![[Pasted image 20250314111216.png]]

## 1.2一对一
例:用户与身份证信息的关系
关系:**一对一关系,多用于单表拆分,将一张表的基础字段放在一张表中,其他字段放在另一张表中,以提高操作效率**
==实现==:在任意一方加入外键,关联另外一方的主键,并且设置外键为唯一的(UNIQUE)

## 1.3多对多
案例:学生和课程的关系
关系:应该学生可以选修多门课程,一门课程也可以供多个学生选择
==实现==:建立第三张中间表,中间表至少包含两个外键,分别关联两方主键
![[Pasted image 20250314113429.png]]


# 2.多表查询
==笛卡尔积==:笛卡尔积乘积是指在数学中,两个集合(A集合和B集合)的所有组合情况(在多表查询时,需要消除无效的笛卡尔积)
* 连接查询:相等于查询A,B交集部分数据
* 外连接
     * 左外连接:查询左表所有数据(包括两张表交集部分数据)
     * 右外连接:查询右表所有数据(包括两张表交集部分数据)
* 子查询

## 2.1连接查询
### 2.1.1内连接
**连接查询:相等于查询A,B交集部分数据**
==隐式内连接:==
```
select 字段列表 from 表1,表2 where 条件...;
```
==显示内连接:==
```
select 字段列表 from 表1 [inner] join 表2 on 连接条件...;
```

```
-- 内连接  
-- A.查询员工姓名,及所属部门名称(隐式内连接实现)  
select tb_dept.name,tb_emp.name from tb_dept,tb_emp where tb_emp.dept_id = tb_dept.id ;  
-- 给表起别名  
select e.name,d.name from tb_emp e,tb_dept d where e.dept_id = d.id;  
  
-- B.查询员工姓名,及所属部门名称(显示内连接实现)  
select tb_dept.name,tb_emp.name from tb_emp inner join tb_dept on tb_emp.dept_id = tb_dept.id;
```

### 2.1.2外连接
**左外连接:查询左表所有数据(包括两张表交集部分数据)**
==左外连接:==
```
select 字段列表 from 表1 left outer join 表2 on 连接条件...;
```
**右外连接:查询右表所有数据(包括两张表交集部分数据)**
==右外连接:==
```
select 字段列表 from 表1 right outer join 表2 on 连接条件...;
```

```
-- 外连接  
-- 左外连接  
select tb_dept.name,tb_emp.name from tb_emp left outer join tb_dept on tb_emp.dept_id = tb_dept.id;  
  
-- 右外连接  
select tb_dept.name,tb_emp.name from tb_emp right outer join tb_dept on tb_emp.dept_id = tb_dept.id;
```

## 2.2子查询
**SQL语句中嵌套select语句,称为嵌套查询,又称为子查询**
_子查询外部语句可以是 insert/update/select中的任意一个,最常见的是select_
```
select * from 表1 where column1 = (select column1 from 表2)
```
 * ==标量子查询==:子查询返回的结果为单个值
 * ==列子查询==:子查询返回结果为一列
 * ==行子查询==:子查询返回结果为一行
 * ==表子查询==:子查询返回结果为多行多列

### 2.2.1标量子查询
**子查询返回的结果是单个值(数字,字符串,日期等),最简单的形式**
常用的操作符:`= <> > >= < <=`
```
-- 1.标量子查询  
-- A.查询在"教研部"所有员工信息  
-- 由于员工表内使用部门id来代替部门名称-故查询教研部员工信息需要拆分成两个步骤完成  
# -- a1.查询教研部的部门id  
# select id from tb_dept where name = '教研部';-- 查询到教研部的部门id为2  
# -- a2.再查询该部门id下的员工信息  
# select * from tb_emp where dept_id = 2;  
  
-- 把两条sql语句合并成一条  
select * from tb_emp where dept_id = (select id from tb_dept where name = '教研部');  
  
-- B.查询在"方东白"入职之后的员工信息  
# -- b1.查询东方白的入职日期  
# select entrydate from tb_emp where name = '方东白';  
# -- b2.查询东方白入职后的员工信息  
# select * from tb_emp where entrydate > '2012-11-01';  
  
-- 将两条sql语句合并成一条变成标量子查询  
select * from tb_emp where  entrydate > (select entrydate from tb_emp where name = '方东白');
```

### 2.2.2列子查询
**列子查询返回的结果是一列(可以是多行)**
常用的操作符:`in,not in等`
```
-- 列子查询  
-- A.查询"教研部"和"咨询部"的所有员工信息  
-- a1查询教研部和咨询部的部门id  
select id from tb_dept where name = '教研部' or name = '咨询部';  
-- a2根据部门信息查询该部门下的所有员工信息  
# select * from tb_emp where dept_id = 2 or dept_id = 3;  
select * from tb_emp where dept_id in (3,2);  
-- 把两条sql语句合并成一条  
select * from tb_emp where dept_id in (select id from tb_dept where name = '教研部' or name = '咨询部');  
-- 括号内语句(select id from tb_dept where name = '教研部' or name = '咨询部')为子查询-返回的是一列多行的结果,所以称为列子查询
```

### 2.2.3行子查询
**行子查询返回的结果是一行(可以是多列)**
常用的操作符:`=,<>,in,not in`
```
-- 行子查询  
-- A.查询与"韦一笑"的入职日期及职位都相同的员工信息  
-- a1查询韦一笑的入职日期及职位  
select entrydate,job from tb_emp where name = '韦一笑';  
-- a2查询与韦一笑入职日期及职位相同的员工信息  
select * from tb_emp where entrydate = '2007-01-01' && job = 2;  
-- 或  
select * from tb_emp where(entrydate,job) = ('2007-01-01',2);  
  
-- 把两条sql语句合并  
select * from tb_emp where entrydate = (select entrydate from tb_emp where name = '韦一笑') && job = (select job from tb_emp where name = '韦一笑' );  
-- 或  
select * from tb_emp where (entrydate,job) = (select entrydate,job from tb_emp where name = '韦一笑');
```

### 2.2.4表子查询
**表子查询返回的结果是多行多列,常作为临时表**
常用的操作符:`in`
```
-- 表子查询  
-- A.查询入职日期是"2006-01-01"之后的员工信息及部门名称  
-- a1查询入职日期是2006-01-01之后的员工信息  
select * from tb_emp where entrydate > '2006-01-01';  
-- 把上述查到的员工信息表作为一张临时表使用  
-- a2查询到员工信息后查询部门及名称  
select e.* , d.name from (select * from tb_emp where entrydate > '2006-01-01')e ,tb_dept d  where e.dept_id = d.id;
```

# 3.事务

## 3.1事务的概念
`事务`是一组操作的集合,它是一个不可分割的工作单位,事务会把所有操作作为一个整体一起向系统提交或者撤销操作请求,即使这些操作`要么同时成功,要么同时失败`
==注意==:默认MySQL的事务是自动提交的,也就是说,当执行一条DML语句,MySQL会立即隐式的提交事务

## 3.2操作
* 开启事务
```
start transaction;/begin;
```
* 提交事务
```
commit;
```
* 回滚事务
```
rollback;
```
先执行`开启事务`,再执行相应的sql语句,sql语句有==错误==,执行`回滚事务`,sql语句==正确==,执行`提交事务`

## 3.3事务的四大特性
==原子性==:事务是不可分割的最小单元,要么全部成功,要么全部失败
==一致性==:事务完成时,必须使所有数据都保持一致状态
==隔离性==:数据库系统提供的隔离机制,保证事务在不受外部并发操作影响的独立环境下运行
==持久性==:事务一旦提交或者回滚,它对数据库中的数据改变就是永久的


# 4.索引

## 4.1索引的概念
`索引(index)`是帮助数据库==高效获取数据==的数据结构
索引的`优点`:1)提高数据查询的效率,降低数据库的IO成本
           2)通过索引列队数据进行排序,降低数据排序的成本,降低CPU消耗
索引的`缺点`:1)索引会占用存储空间
          2)索引大大提高了查询效率,同时却也降低了insert,update,delete的效率


## 4.2索引结构
MySQL数据库支持的索引结构有很多,如:`Hash索引,B+Tree索引,Full-Text索引等`,我们平常所说的索引如果没有特别知名都是指默认的==B+Tree==结构组织的索引

* B+Tree(多路平衡搜索树)
![[Pasted image 20250326110718.png]]
例:**找53,从第一页判断53大于38小于67,走指针p2到第三页,53大于47小于55走第二页的指针p2,在第六页找到53**
==B+Tree树的三个重要的特点:==
1) 每一个节点,可以存储多个Key(有n个Key,就有n个指针)
2) 所有数据都存储在叶子节点,非叶子节点仅用于索引数据
3) 叶子节点形成了一颗双向链表,便于数据的排序及区间范围查询

## 4.3索引的操作语法
* ==创建索引==
```
create [unique] index 索引名 on 表名(字段名,...);
```

```
 -- 创建索引:为tb_emp表的name字段建立一个索引  
create index idx_emp_name on tb_emp(name);  
-- 索引重命名规则:idx(index简写)_表名_字段名
```

* ==查看索引==
```
show index from 表名;
```

*  ==删除索引==
```
drop index 索引名 on 表名;
```

==注意:==
1) 创建唯一索引时才需要添加`unique`
2) 数据库中设置为主键的字段会自动创建索引,这个索引称为`主键索引`
3) 添加了`unique`约束后,数据库会为其添加`唯一索引`
![[Pasted image 20250326112447.png]]