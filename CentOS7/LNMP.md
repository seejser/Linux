##centOS7安装PHP7.1+MYSQL5.7
1.安装软件源
添加epel源
```
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY*
rpm -Uvh http://mirrors.rit.edu/fedora/epel//7/x86_64/e/epel-release-7-9.noarch.rpm

```
添加remi源
```
rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm

```
安装并更新软件

安装yum-config-manager实用程序
```
yum -y install yum-utils
yum -y update

```
更新完成后，就可以安装所需要的PHP版本了。
2.安装PHP
以上准备工作完成后，就可以安装所需的PHP版本了。
```
yum-config-manager --enable remi-php71
yum -y install php php-opcache
```
安装前可尝试
`
yum search php71
`
搜索可安装的软件包。
完成后还需要添加PHP常用扩展：
```
yum -y install php-mysql php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-soap curl curl-devel
```
3.启动php-fpm
第一次通过systemctl启动PHP服务时需要先将php-fpm服务enable：
```
systemctl enable php-fpm.service
systemctl start php-fpm.service
```

