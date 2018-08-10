# MYSQL 添加用户
1.add user
##### 以root用户登录数据库，运行以下命令：
```
create user zhangsan identified by 'zhangsan';
```
上面的命令创建了用户zhangsan，密码是zhangsan。在mysql.user表里可以查看到新增用户的信息：
```
use mysql;
select host,user from mysql.user;
```
2.authorize
命令格式：grant privilegesCode on dbName.tableName to username@host identified by "password";
```
grant all privileges on zhangsanDb.* to zhangsan@'%' identified by 'zhangsan';
flush privileges;
```
上面的语句将zhangsanDb数据库的所有操作权限都授权给了用户zhangsan。

3.在mysql.db表里可以查看到新增数据库权限的信息：
```
select User,Db,Host,Select_priv,Insert_priv,Update_priv,Delete_priv from mysql.db where User='Garth';
```
4.也可以通过show grants命令查看权限授予执行的命令：
```
show grants for 'zhangsan';
```
