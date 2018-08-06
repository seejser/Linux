# CentOS7下安装mysql5.7
1、安装YUM Repo

由于CentOS 的yum源中没有mysql，需要到mysql的官网下载yum repo配置文件。
```
wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
```
然后进行repo的安装：
```
rpm -ivh mysql57-community-release-el7-9.noarch.rpm
```
执行完成后会在/etc/yum.repos.d/目录下生成两个repo文件mysql-community.repo mysql-community-source.repo


2、安装MySQL

使用yum命令即可完成安装
```
yum install mysql-server
```
启动msyql：
```
systemctl start mysqld #启动MySQL
```
配置MySQL

获取安装时的临时密码：
```
grep 'temporary password' /var/log/mysqld.log
```
登录：
```
mysql -u root -p
```
登录成功后修改密码：
```
set password=password("yourpassword");
```
 设置安全选项：
```
mysql_secure_installation
```
其他设置：
```
systemctl stop mysqld #关闭MySQL
systemctl restart mysqld #重启MySQL
systemctl status mysqld #查看MySQL运行状态
systemctl enable mysqld #设置开机启动
systemctl disable mysqld #关闭开机启动
```
 3、其他配置
开启远程控制

MySQL默认是没有开启远程控制的，必须添加远程访问的用户


```
grant all privileges on 数据库名.表名 to 创建的用户名(root)@"%" identified by "密码"; # 数据库名.表名 如果写成*.*代表授权所有的数据库 

flush privileges; #刷新刚才的内容
```

#如：
```
grant all privileges on *.* to root@"113.64.243.1" identified by "123456789";
```

@ 后面是访问mysql的客户端IP地址（或是 主机名） % 代表任意的客户端，如果填写 localhost 为本地访问（那此用户就不能远程访问该mysql数据库了）。

同时也可以为现有的用户设置是否具有远程访问权限。

配置默认编码为utf8：
```
vi /etc/my.cnf
```
#添加
```
[mysqld]
character_set_server=utf8
init_connect='SET NAMES utf8'
```
其他默认配置文件路径： 

配置文件：/etc/my.cnf 
日志文件：/var/log//var/log/mysqld.log 
服务启动脚本：/usr/lib/systemd/system/mysqld.service 
socket文件：/var/run/mysqld/mysqld.pid
