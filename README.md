# Linux
1. 查看MySQL版本等信息
```
mysql --help | grep Distrib 
```
2.如何生成SSH密钥？
```
ssh-keygen -t rsa -C " youremail@example.com"
```
成功后显示如下信息：
```
Your identification has been saved in /c/Users/dir/.ssh/id_rsa.
Your public key has been saved in /c/Users/dir/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:wp3oeluctx4VLy9PPbCzCPA7rnNoHHVRDZZbdU0Nj4Y your_email@example.com
```
3.如何添加SSH密钥？

查看你的 public key，在命令行终端输入：
```
cat ~/.ssh/id_rsa.pub
```
以下为显示的密钥（示例）：
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCx/QMSjVSLKmHC0gNkVqjt59LdTkL1/3EJAQEIw
TtlFNqTGAjTQMdZByDEfYacTfrsjnabUfUXgXYLd4RHv1/HYWcDq/LQDqT7x8xEuyGnC8RX980/me
5O5DhadUT3q3plppHX2MaT/qhQPmBz9H/fUGpkcL8nLJS3xCgXh4psC4us3Wnc1XUr7u1AEPZmmWc
NVfehZ2cpr8DnD0MoWc2elKUQFmRuq3TyKnSvZRqPZ4OszmQ251mJEXcAZTUnHQQ1zszKSjO/oeY7
1XGOMOACqSCDBIw1cyMw5QTJ73vgxDOvMGMOntr/HuJbGmAevinl062/ph+47zNFRafTPm8r 9000
00000@qq.com
```
4.zip打包当前目录
```
zip -r ./a.zip ./*
```

5.查询文件大小M为单位

```
du -h --max-depth=1 work/testing
```

6.linux 检测远程端口是否打开

```
telnet baidu.com 80
```
显示：
```
Trying 123.125.114.144...
Connected to baidu.com (123.125.114.144). #==>出现Connected表示连通了，说明百度的80端口开放的
Escape character is '^]'. #==>ctrl+]退出此地。
^]
telnet> quit
Connection closed.
```

如果写脚本通过telnet检查端口可以用下面的方法：
```
[root@oldboy ~]# echo -e "\n"|telnet baidu.com 80|grep Connected
Connection closed by foreign host.
Connected to baidu.com (123.125.114.144).
```

二、查看Linux系统版本的命令（3种方法）

1、cat /etc/issue，此命令也适用于所有的Linux发行版。

　　[root@S-CentOS home]# cat /etc/issue
　　CentOS release 6.5 (Final)
　　Kernel \r on an \m

2、cat /etc/redhat-release，这种方法只适合Redhat系的Linux：

　　[root@S-CentOS home]# cat /etc/redhat-release
　　CentOS release 6.5 (Final)

 

3、lsb_release -a，即可列出所有版本信息：

　　[root@S-CentOS ~]# lsb_release -a
　　LSB Version: :base-4.0-amd64:base-4.0-noarch:core-4.0-amd64:core-4.0-noarch:graphics-4.0-amd64:graphics-4.0-noarch:printing-4.0-amd64:printing-4.0-noarch
　　Distributor ID: CentOS
　　Description: CentOS release 6.5 (Final)
　　Release: 6.5
　　Codename: Final

 

三、查看Linux内核版本命令（两种方法）：

1、cat /proc/version

　　[root@S-CentOS home]# cat /proc/version
　　Linux version 2.6.32-431.el6.x86_64 (mockbuild@c6b8.bsys.dev.centos.org) (gcc version 4.4.7 20120313 (Red Hat 4.4.7-4) (GCC) ) #1 SMP Fri Nov 22 03:15:09 UTC 2013

2、uname -a

　　[root@S-CentOS home]# uname -a

　　Linux S-CentOS 2.6.32-431.el6.x86_64 #1 SMP Fri Nov 22 03:15:09 UTC 2013 x86_64 x86_64 x86_64 GNU/Linux
  
3.Ubuntu中程序崩溃，杀死进程方法

```
//查找进程：
sudo netstat -antup

//杀死进程：

sudo kill 123

kill -9 pid 命令,来强制杀掉
```
