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
