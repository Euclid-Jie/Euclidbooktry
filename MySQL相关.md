MSQL的一级数据结构为数据库（dataBase），下级为数据表（tables）类比于MongoDB的collection

## MySQL 安装

参照教程[(103条消息) Windows安装mysql详细步骤（通俗易懂，简单上手）_华夏之威的博客-CSDN博客](https://blog.csdn.net/weixin_43423484/article/details/124408565)

## 登录MySql

默认开机启动，如果没有启动服务，则使用服务台进行启动

命令行进行登录，提示输入密码后，输入密码123456

```shell
mysql -uroot -p
```

退出，注意MySQL的语句都是英文分号结束

```shell
exit;
```

## CMD窗口操作

### 数据库有关操作

1.查询时间：select now();

2.查询当前用户：select user();

3.查询数据库版本：select version();

4.列出数据库：show databases;

5.选择数据库：use databaseName;

6.建立数据库：create database databaseName;

7.查看新创建的数据库信息：show create database databaseName;

8.删除数据库：drop database databaseName;

### 数据表有关操作

1.查看数据表存储引擎：show engines；

2.列出表格：show tables；

3.创建表：CREATE TABLE tableName(
    c_num int (11) not null  unique primary key auto_increment,
    c_name varchar (50),
    c_contact varchar (50),
    c_city varchar (50),
    c_birth datetime not null
);

4.查看表结构：desc tableName;

5.显示表格列的属性：show columns from tableName;

6.修改字段类型：alter table tableName modify fieldName newFieldType; 

7.字段改名：alter table tableName change oldFieldName newFieldName newFieldType; 

8.表改名：alter table oldTableName rename newTableName;

9.复制表：create table tableName2 select * from ttableName1;

10. 插入表中一行记录：insert into tableName values ("value1","value2","value3"......);

11. 删除表中一行记录：delete from tableName where columnName=value; //不加where将删除全部数据

12. 更新表中一行记录：update tableName set columnName=value where columnName=value; 

13. 查询表中所有记录：select * from tableName;

14.删除表：drop TABLE tableName;

### 用户操作

创建新用户

```mysql
create user 'user01' @'localhost' identified by 'user01';
flush privileges;  #刷新权限
```

删除用户

```mysql
drop user ‘user01’@’localhost’;
```

查看所有用户

```mysql
select user,host from mysql.user;
```

### MySql语法基础

[MySQL 数据类型 | 菜鸟教程 (runoob.com)](https://www.runoob.com/mysql/mysql-data-types.html)

语句执行顺序

1. FROM, including JOINs
2. WHERE
3. GROUP BY
4. HAVING
5. WINDOW functions
6. SELECT
7. DISTINCT
8. UNION
9. ORDER BY
10. LIMIT and OFFSET

插入语句

```sql
insert 北京师范大学微博评论
(mid, time, nick_name, content, 转发数, 评价数, 点赞数)
VALUE
(11111,'20201201','Test','Test',1,1,1);
```

查询语句

```sql
select * from 北京师范大学微博评论
where 点赞数 =1
limit 10 offset 10
```



## DataGrip使用MySql

### 连接数据库

![image-20230421104844253](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/202304211048464.png)

### 由csv导入数据

- 长int得使用bigint类型

![image-20230421104918552](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/202304211049856.png)

### 
