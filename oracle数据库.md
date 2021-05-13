# oracle常用sql

> ​		[结构化查询语言](https://baike.baidu.com/item/结构化查询语言/10450182)(Structured Query Language)简称SQL，结构化查询语言是一种数据库查询和[程序设计语言](https://baike.baidu.com/item/程序设计语言/2317999)，用于存取数据以及查询、更新和管理[关系数据库系统](https://baike.baidu.com/item/关系数据库系统)；

### 	1.增、删、改、查

​			以创建的student表为例：

```sql
create table student(
	stu_name varchar(10),
	stu_age number(3),
	stu_sex char(4),
    stu_id number(38)
);
```

​	

### 	  2.增加数据 

​			添加数据需要注意，*添加的数值需以字段类型相对应*，有两种方式：

​					选择字段进行添加数据；

```sql
insert into student (stu_name,stu_age) 
values('lou',21);
```

​					全字段添加数据；

```sql
insert into student values('lou',21,'男',123);
```



### 	3.删除数据/表

​				删除数据/表需要注意，分情况判断：

​				清空表数据：

```sql
delete table student;
```

​				按条件删除不需要的数据：

```sql
delete table student;
	where stu_name='lou' 
```

​				删除表：

```sql
drop table student;
```

注意：删除表之后表及数据都会被删除

​	

### 	4.查询数据

​					查询数据中配合常用的sql函数（以student表为例）：
$$
max();//求最大值
min();//求最小值
avg();//求平均值
count();//求其条数
sum();//求和
distinct();//去重
order by ;//排序
group by;//分组
having ;//组函数条件
left/right/full join... ...on   //左、右、全连接
rownum //分页关键字
$$
​	

##### 			1.查询表数据

```sql
select * from student ;
```

​			//注意：‘’*“ 代表全字段，select 语法后跟展示的字段名称，

​														from语法后面跟表名，表示来之那张表。

##### 			2.查询student表中学生的数量

```sql
select count(*) from student;
```

##### 			3.查询student表中学生的年龄的和、平均值、按照学生年龄从小到大排序

```sql
select sum(stu_age) from student;
select avg(stu_age) from student;
select * from student order by stu_age --注意：order by 默认升序 ace 看2不书写，降序 desc
```

##### 			4.查询student表中最大/小年龄的学生

```sql
select max(stu_age) from student;
select min(stu_age) from student;
```

##### 			5.将student表中的学生以年龄来分组，求其组人数大于三人以上的年龄有哪些

```sql
select stu_age,count(stu_age) from student 
		group by 
			stu_age  --注意：group by 的使用中函数后面的字段必须和select语法后面的字段一致，组函数可以忽略--例如：'count(),max(),min(),avg()... ...'
         having 
         	count(stu_age)>=3;--注意：having 函数条件必须是select语法后面有的组函数
      
```

##### 			6.表连接查询

```sql
--创建表class
	create table class(
    	cla_name varchar(20),
        cla_id number(38),
        stu_id number(38)
    );
 --student表与class表连接
 select t1.*,t3.* from student t1 --给student表起别名 t1
 			left join      --表连接的方式
 				class t2   --被连接的表
 			on 				--表连接关键字
 				t1.stu_id=t2.stu_id --两张表连接的关键字依据
 				
 --left join 连接的结果呈现会有的一种情况：若被连接的表的字段为null值，则说该stu_id对应的在被连接表中无数据，			
    
```

​			

```txt
typora阅读软件安装地址：
	https://www.typora.io/#windows
```

