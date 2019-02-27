一、安装vsftpd
　　1、安装vsftpd： 
```
yum install vsftpd -y
```

　　2、启动vsftpd： 
```
  systemctl start vsftpd
```

　　3、设置开机启动：
```
  systemctl enable vsftpd
```

　　4、创建ftp根目录：
```
  mkdir -p /ftpserver

```

  5.查看Vsftp状态
```
systemctl status vsftpd

```
二、设置配置文件：vim /etc/vsftpd/vsftpd.conf 
```
　　listen=NO 　　　　　　　　　　　　　　　　// 如此条改为了，等于YES也行
　　listen-address=172.16.0.236	　　　　	　　	// 绑定本机IP
　　#禁止匿名访问
　　anonymous_enable=NO
　　anon_upload_enable=NO
　　anon_mkdir_write_enable=NO
　　anon_other_write_enable=NO


　　chroot_list_enable=NO	　　　　　　　　　　// 不允许用户离开自己的主目录
　　chroot_list_file=/etc/vsftpd.chroot_list　　  // 虚拟用户列表，每行一个用户名
　　local_enable=YES	　　　　　　　　　　	　　	// 允许本地用户访问
　　write_enable=YES	　　　　　　　　　　　　 // 允许本地用户写入
　　local_umask=022	　　　　　　　　　　　　	// 上传后的文件的默认掩码
　　chroot_local_user=YES	　　　　　　　　　　	// 禁止本地用户离开自己的主目录
　　pam_service_name=vsftpd.vu	　　　　　　	// 权限验证需要的加密文件
　　guest_enable=YES	　　　　　　　　　　　　	// 开启虚拟用户功能
　　guest_username=ftp	　　　　　　　　　　　// 虚拟用户的宿主目录
　　virtual_use_local_privs=YES	　　　　　　  	// 用户登录后操作目录和本地用户权限一样
　　user_config_dir=/etc/vsftpd/vconf	　　　　// 虚拟用户主目录设置文件
　　allow_writeable_chroot=YES	　　　　　　	// 允许写入用户主目录，这条特别重要
```
三、添加用户，并创建用户目录

　　1、vim /etc/vsftpd.chroot_list，添加两个用户如进去，分别为：

　　user1

　　user2

　　2、mkdir -p  /ftpserver/user1  /ftpserver/user2 // 创建用户目录

　　3、chmod –R 755 /ftpserver/user1 /ftpserver/user2 // 修改目录权限

四、设置用户密码和数据库

　　1、echo -e "user1\n123456\nuser2\n123456" >/etc/vsftpd/vusers.list 　　// 创建用户和密码

　　2、cd /etc/vsftpd  　　　　　　　　　　　　　　　　　　　　　　　　　　　　

　　3、db_load  –T  –t  hash  –f  vusers.list  vusers.db  

　　4、chmod  600  vusers.*

五、指定认证方式，添加如下内容 vim /etc/pam.d/vsftpd.vu

　　#%pam-1.0

　　auth　　　required　　pam_userdb.so　　db=/etc/vsftpd/vusers

　　account　 required　　pam_userdb.so　　db=/etc/vsftpd/vusers　

六、创建文件并指定ftp用户目录

　　1、mkdir –p /etc/vsftpd/vconf

　　2、cd /etc/vsftpd/vconf

　　3、touch user1 user2
　　4、添加内容，vim user1

　　　　local_root=/ftpserver/user1

　　5、vim user2

　　　　local_root=/ftpserver/user2

七、重启服务即可访问FTP：systemctl  restart vsftpd

八、添加新用户

　　1、创建新用户目录：mkdir -p /ftpserver/test1
　　
　　2、	添加用户名，vim /etc/vsftpd.chroot_list，添加内容： test1
　　　
　　3、修改目录权限Chmod –R 755 /ftpserver/test1

　　4、添加用户及密码，vim /etc/vsftpd/vusers.list
　　　　test1　　　　　　//用户名
　　　　a123456　　　　//密码
　　5、设置数据库
　　　　cd /etc/vsftpd
　　　　db_load –T –t hash –f vusers.list vusers.db
　　　　chmod 600 vusers.*
　　6、创建文件名文件，并指定用户目录
　　　　touch /etc/vsftpd/vconf/test1
　　　　vim /etc/vsftpd/vconf/test1
　　　　local_root=/ftpserver/test1

　　7、重启服务即可：systemctl  restart vsftpd

注意事项：

1、如让用户有写入权限，则需给用户目录添加其它用户的写入权限： chmod o+w /ftpserver/jefflee
2、如还访问不了，记得设置(打开：vim /etc/selinux/config)：SELINUX=permissive
