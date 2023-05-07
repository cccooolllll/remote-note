```mysql
mysql -uroot -ppassword	//登录MySQL
exit	//退出MySQL
show databases;	//展示所有数据库
use %sqlname%;	//使用某个数据库
create database %sqlname%;	//创建一个数据库
show tables;	//使用某个数据库，展示这个数据库里的表
source 文件路径	//导入数据库
select * from 表名;	//查询表所有内容
desc 表名;	//查询表结构
select database();	//查看当前在哪个数据库
```

### DQL（Data Query Languag）

数据查询语言，用来查询数据库中表的记录(数据)

#### 简单查询

```
//1.注册驱动
Class.forName("com.mysql.cj.jdbc.Driver");
//2.获取连接
Connection connection = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/atguigu?user=root&password=password");
//3.编写SQL语句结果，动态值的部分使用?
//4.创建preparedstatement，并且传入sql语句结果
//5.占位符赋值
//6.发送sql语句
//DML
//7.输出结果
//8.关闭资源
```

字段可以进行简单运算
```mysql
select 字段名 from 表名;	//从一个表中查询一个字段
select 字段名1,字段名2 from 表名;	//在表中查询多个字段
select 字段名 as 别名 from 表名;	//从表中查询一个字段并为其起别名，但不会更改真实名
```

#### 条件查询

```
select
	字段1,字段2,字段3
from
	表名
where
	条件;		//带条件查询字段
	
=
!=
<
<=
>
>=
between ... and ...		//两个值之间
is null		//null值
is not null //不为null值
and	//并且
or	//或者
in //包含
like //模糊查询
	%	//匹配任意多个字符
	_	//下划线，一个下滑线只匹配一个字符
	
having	//最后再次过滤
```

#### 排序

```mysql
select
	字段1,字段2,字段3
from
	表名
order by
	字段;			//默认升序
	
	字段 desc;	//降序
	
	字段1 asc, 字段2 asc;	//根据字段1p,如果相等再按照字段2排序.
```

#### 单行处理函数

```mysql
case..when..then..when..then..else..end	//选择并处理
//示例
select ename,job,sal as oldsal,(case job when 'MANAGER' then sal * 1.1 when 'SALESMAN' then sal * 1.5 else sal end) as newsal from emp;
/*
| ename  | job       | oldsal  | newsal
+--------+-----------+---------+---------
| SMITH  | CLERK     |  800.00 |  800.00
| ALLEN  | SALESMAN  | 1600.00 | 2400.00
| WARD   | SALESMAN  | 1250.00 | 1875.00
| JONES  | MANAGER   | 2975.00 | 3272.50
| MARTIN | SALESMAN  | 1250.00 | 1875.00
| BLAKE  | MANAGER   | 2850.00 | 3135.00
| CLARK  | MANAGER   | 2450.00 | 2695.00
*/

str_to_date('字符串日期','日期格式')	/*str_to_date('1111-11-11','%Y-%m-%d')*/
```

#### 多行分组处理函数

```mysql
count	//统计个数
sum		//求和
max		//最大值
min		//最小值
avg		//平均值
```

#### 分组查询

```mysql
select
	...
from
	...
group by
	... , ... , ...
```

```mysql
distinct	//去除重复内容
	 示例:select distinct deptno from emp;
```

#### 连接查询

```mysql
//多张表联合起来查询数据,被称为连接查询
根据表连接方式分类:
	内连接:
		等值连接
		非等值连接
		自连接
	外连接:
		左外连接	left	与right相反
		右外连接	right	表示将join关键字右边的表看作主表,主要是为了将这张表数据全部查询出来,其次才起到关联查询左边的表,outer可省略.
			select 
				e.ename,d.dname 
			from 
				emp e right /*outer*/ join dept d 
			on 
				e.deptno = d.deptno;
	全连接
```

```mysql
//等值连接
select 
 	...
from 
 	表a
join 
 	表b 
on 
 	a和b的连接条件
where
	筛选条件;
```

```mysql
select 
 	...
from 
 	表a
join 
 	表b 
on 
 	a和b的连接条件
join
	c
on
	a和c的连接条件
join
	d
on
	a和d的连接条件
```

#### 子查询

```mysql
select
	..(select).
from
	..(select).
where
	..(select).
	
```

```mysql
union	//将两个结果合在一起
limit	//将查询结果集的一部分取出来,通常使用在分页查询中
	limit startIndex,length
	
	select
		ename,sal
	from
		emp
	order by
		sal desc
	limit 5;	//取前五
```

```mysql
DQL语句命令语句顺序
select
	...
from	
	...
where	
	...
group by	
	...
having	
	...
order by	
	...
limit	
	...
执行顺序
	1.from
	2.where
	3.group by
	4.having
	5.select
	6.order by
	7.limit
```

### DDL（Data Definition Language）

**数据定义语言，例如建数据库、建表等**

```mysql
create	//创建表
	create table 表名(字段名1 数据类型, 字段名2 数据类型, 字段名3 数据类型);
	create table 表名1 as select * from 表名;将查询结果当作一张表新建,也可以完成表的复制.
drop	//删除表
	drop table 表名;	//当这张表不存在时会报错
	drop table if exists 表名;	//不报错
alter	//修改表字段
	alter table 表名 drip 字段名；	//使用了ALTER命令及DROP子句来删除以上创建表的某个字段：
	alter table 表名 add 字段名 指定字段数据类型；	//添加字段到表字段的末尾；
	alter table 表名 modify 字段名 要更改字段数据类型；	//修该字段的数据类型；
	
truncate	//删除表中数据,物理删除,删除效率高,不支持回滚
	truncate table 表名;
```

#### create

```mysql
create	//创建表
	create table 表名(字段名1 数据类型, 字段名2 数据类型, 字段名3 数据类型);
	create table 表名1 as select * from 表名;将查询结果当作一张表新建,也可以完成表的复制.
```

```mysql
//数据类型
varchar		//可变长度的字符串,会根据实际的数据长度动态的改变长度
char		//定长字符串,分配固定长度空间存储数据
int			//
bigint		//
float		//
double		//
date		//短日期
datetime	//长日期,带时分秒
clob		//字符大对象,最多可以存储4G的字符串
blob		//二进制大对象,用来存储图片,声音,视频,需使用IO流
```

#### 约束

```mysql
not null	非空约束	//没有表级约束
unique		唯一性约束
primary key	主键约束	
	//特征：not null + unique	主键只能由一个
	id int primary key auto_increment,	//mysql自动维护的主键，从1开始自增
foreign	key	外键约束
	//引用其他表的数据对本表进行约束，使本表只能，被引用的其他表是父表，本表是子表
示例：create table t_class(
    	classno int primary key,
        classname varchar(255)
    );
    create table t_student(
    	no int primary key auto_increment,
        name varchar(255),
        cno int,
        foreign key(cno) references t_class(classno)	//引用t_class表的classno数据
    );
//建表的时候对字段内容进行约束
//没有添加在列的后面,这种约束被称为表级约束
//多个约束可以约束同一个字段
示例:create table t_test(
    	no int unique,
    	id int primary key,
    	name varchar(255) not null,
    	email varchar(255),
    	unique(name,email) //指两个字段联合具有唯一性,只有两个都相同才报错
	);
```



### DML（Data Manipulation Language）

数据操纵语言，最常用的增删改查就属于DML，操作对象是数据表中的记录；

```mysql
insert	插入	可插入多条记录
	insert into 表名(字段名1,字段名2,字段名3...) values(值1,值2,值3)(值1,值2,值3)...;
update	更新	//没有条件限制会导致所有数据全部更新
	update 表名 set 字段名1=值1,字段名2=值2,字段名3=值3...where 条件;
	/*示例:update t_student set name ='jack',email = 'jack@1.com' where no = 2;*/
delete	删除	//没有条件限制会导致所有数据全部删除
	delete from 表名 where 条件;
```

#### delete删除

```mysql
delete	删除	//没有条件限制会导致所有数据全部删除
	delete from 表名 where 条件;
//表中的数据被删除了,但是这个数据再硬盘上的真实存储还在
//删除效率低
//支持回滚,可以恢复数据
truncate	//物理删除,删除效率高,不支持回滚	D
	truncate table 表名;
```



### DCL（Data Control Language）

数据控制语言，如Grant、Rollback等等，常见于数据库安全管理，多数人一般很少用。



### 事务

完整的业务逻辑，只有DML语句才有事务，其他语句和事务无关。
只有DML语句才是对数据库表中数据进行操作的。

```mysql
commit;		//提交事务
	mysql默认自动提交事务，每执行一条DML语句，则提交一次
rollback;	//回滚事务	
	只能回滚到上次提交的时间点
	关闭mysql自动提交机制：在想要回滚的时间点之前执行start stansaction
```

**事务的4个特性**

- 原子性
- 一致性
- 隔离性
- 持久性

**事务隔离级别**

- 读未提交	read uncommitted
- 读已提交    read committed
- 可重复性读 repeatable read
- 序列化        serializable

### 索引

```mysql
create [unique] index 索引名 on 表名(字段名,...);//ch
show index from 表名;//查看索引
drop index 索引名 on 表名;//删除索引
```

