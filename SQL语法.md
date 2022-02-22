### SQL
- SQL分类  
| 分类 | 全称 | 说明 |
| :---: | :---: | :---: |
| DDL | Data Definition Language | 数据定义语言,用来定义数据库对象(数据库,表,字段) |
| DML | Data Manipulation Language |数据操作语言,用来对数据库表中的数据进行增删改|
| DQL | Data Query Language | 数据查询语言,用来查询数据库中表的记录|
| DCL | Data Control Language | 数据控制语言,用来创建数据库用户、控制数据库的访问权限|

- DDL
    - **查询**
       查询所有数据库

       ` show databases; `
    
       查询当前数据库
    
       `select database();`
    
       查询当前数据库的所有表
    
       `show tables;`
    
       查询表结构
    
       `desc 表名;`
    
       查询指定表的建表语句
    
       `show create table 表名;`  
       
       ----
    
    - **创建**
      
       创建数据库
       
       `create database [if not exists] 数据库名 [default charset 字符集] [collate 排序规则]`
       
       创建表
       
       ```mysql
       create table 表名(
       	字段1 字段1类型[comment 字段1注释],
           字段2 字段2类型[comment 字段2注释],
           ...
       )[comment 表注释]
       ```
       
       ----
       
    - **删除**

       删除数据库

       `drop database [if exists] 数据库名;`
       
       删除表
       
       `drop table [if exists] 表名;`
       
       删除表并重新创建该表
       
       `truncate table 表名;`
       
       
       删除字段
       
       `alter table 表名 drop 字段名;`
       
       
       ----
    - **使用**
    
      `use 数据库名`
    
      ----
    - **修改**
      
       添加字段
       
       `alter table 表名 add 字段名 类型 [comment 注释] [约束]`
       
       修改数据类型
       
       `alter table 表名 modify 字段名 新数据类型;`
       
       修改字段名和数据类型
       
       `alter table 表名 change 字段名 新字段名 新数据类型;`
       
       修改表名
       
       `alter table 表名 rename to 新表名;`
       
       ---
    
- DML
    - **插入数据(INSERT)**
      **(在插入字符串和日期型数据必须包含在引号内)**
      
       给指定字段添加数据
      
       `insert into 表名 (字段名1,字段名2,...) values(值1,值2,...);`
      
       给全部字段添加数据
      
       `insert into 表名 values (值1,值2,...);`
      
       批量添加数据
      
       `insert into 表名 (字段1,字段2,...) value (值1,值2,...),(值1,值2,...),...;`
      
       `insert into 表名 value (值1,值2,...),(值1,值2,...),...;`
      
      ---
      
    - **修改数据(UPDATA)**
      
       `update 表名 set 字段名1=值1,字段名2=值2,... [where 条件];`
       
       ---
       
    - **删除数据(DELETE)**
      
       `delete from 表名 [where 条件];
       
       ---

- DQL
    - **DQL语法**
       ```mysql
       select
       	字段列表
       from
       	表名列表
       where
       	条件列表
       group by
       	分组字段列表
       order by
       	排序字段列表
       limit
       	分页参数
       ```
    - **DQL-基本查询**
       
       查询多个字段
       
       `select 字段1,字段2,... from 表名;`
       
       `select * from 表名;`
       
       设置别名
       
       `select 字段1 [as 别名1],... from 表名;`
       
       去除重复记录
       
       `select distinct 字段列表 from 表名;`
       
       
       