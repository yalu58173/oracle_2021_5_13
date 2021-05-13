# oracle

#### 		oracle数据库中临时空间表会出现的问题

##### 			1.temp空间表

​				

```sql
--无法通过temp表 该问题是由于操作的SQL语句使用函数大量查询表数据造成
--http://blog.chinaunix.net/uid-25492475-id-3438089.html
--1.重新创建临时表空间temp  
    create temporary tablespace TEMP TEMPFILE 'C:\oracle\oradata\lzmes\temp01.dbf' SIZE 512M REUSE AUTOEXTEND ON NEXT 1M MAXSIZE UNLIMITED; 

--2.重置缺省临时表空间为新建的temp表空间
    alter database default temporary tablespace temp; 

--3.删除中转用临时表空间  
    drop tablespace temp2 including contents and datafiles; 

--4.重新指定用户表空间为重建的临时表空间  
    alter user '数据库用户名' temporary tablespace temp;
```

​			

##### 		2.system表空间

```sql
--system空间表问题是由于导入表/表数据中可能会出现的问题，
--https://www.bbsmax.com/A/amd06vM6Jg/
--为SYSTEM表空间增加一个数据文件SYSTEM02.DBF

 ALTER TABLESPACE "SYSTEM" ADD DATAFILE 'dbf目录路径' SIZE 500M AUTOEXTEND ON NEXT 50M MAXSIZE UNLIMITED;
```

