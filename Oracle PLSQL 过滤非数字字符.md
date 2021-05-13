# Oracle PL/SQL 过滤非数字字符

​	

```txt
对此Oracle提供了translate(a, b, c)函数：

a,b,c三个参数均是字符串
当a,b,c中任一个为NULL时，返回NULL。
否则，对a中每个字符x、在b中查找：
如找不到，则追加x到返回值中，
如找到，则再尝试从c中取对应位置的字符y（例如x出现在b中、是第6个字符，则从c中也取第六个字符，若c不足6个字符，则y为NULL）
如y不为NULL，追加y到返回值中
如y为NULL，忽略x
```

```sql
select translate('a1e2c3z', '#0123456789', '#') from dual;
--然后将f作为过滤串再滤一次，即可得到纯数字串（拼接一个0前缀保证非空，避免返回NULL），组合起来：
	--dual:哑表，在没有创建表及没有表的情况下默认的一张表，该表无任何数据，多适用于测试数据。

select translate( 'a1e2c3z', '0' || translate('a1e2c3z', '#0123456789', '#'), '0') from dual;

```



```sql
/*
	例：创建dual01表，insert 数据带有字符和数字的
*/
create table dual01(
    name varchar(10)--luyiao123
)
insert into dual01 values('luyiao123')
insert into dual01 values('456')
insert into dual01 values('luyiao23')


select translate( name, '0' || translate(name, '#0123456789', '#'), '0') from dual01;
```



![](F:\01.PNG)



##### 	以上的方法只是过滤掉每个值中的非数字字符，so 每个值都会留下数值，建议使用以下方法：

```sql
select * from dual01 where regexp_like(name,'^([0-9]+)$');
--该sql语句是只保留数字的数值
```



<img src="F:\dual01表查所有.PNG" style="zoom:75%;" />

<img src="F:\捕获.PNG" style="zoom:75%;" />

```sql
select * from dual01 where ASCIISTR(name) like '%\%';
--运用ASCIISTR函数来查询数值中带有汉字的数值
```

<img src="F:\ASCIISTR函数获取带有汉字的值.PNG" style="zoom:75%;" />

# Oracle中REGEXP_LIKE与LIKE的区别？

```
https://zhidao.baidu.com/question/814655531885514772.html
https://www.jb51.net/article/38426.htm
```

```sql

```



# [:alnum:]和[:digit:]的区别是什么？

```sql
--[:alnum:]代表的是[:alpha:]和[:digit:]，即字母和数字；

--[:digit:]代表的是纯数字。
--sql使用时书写格式必须为：[[:digit:]]
```

注意事项：数值‘0’与‘0.00’  number数字会呈现为‘0’，varchar数字会呈现为‘0.00’

​		