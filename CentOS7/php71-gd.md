# centos7 上为php-fpm安装gd扩展库

1.安装完php71 检查
```
php71 -v
```
2.通过phpinfo()发现么有PHP71-gd,然后安装

3.查看可以安装的程序：
```
yum list | grep gd 
```
4.找到安装版本：php71-php-gd.x86_64 
```
yum install -y php71-php-gd.x86_64 
```
5.重启后检查phpinfo
```
systemctl restart php71-php-fpm
nginx -s reload
```
