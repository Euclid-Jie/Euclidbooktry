## MySQL 安装

参照教程[(103条消息) Windows安装mysql详细步骤（通俗易懂，简单上手）_华夏之威的博客-CSDN博客](https://blog.csdn.net/weixin_43423484/article/details/124408565)

## 用户操作

### 创建新用户

```mysql
create user 'user01' @'localhost' identified by 'user01';
flush privileges;  #刷新权限
```

### 删除用户

```mysql
drop user ‘user01’@’localhost’;
```

### 查看所有用户

```mysql
select user,host from mysql.user;
```

