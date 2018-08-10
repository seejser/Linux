# [mysql报错]Invalid default value for 'create_date' timestamp field
## 问题
最近遇到一个这样的问题，新建数据库表的时候 提示 错误如下
```
Invalid default value for 'create_date' timestamp field
```
写入语句如下：
```
`created_time` timestamp NOT NULL DEFAULT '0000-00-00 00:00:00' COMMENT '插入时间'
```
错误大致的意思 就是不能为 timestamp字段设置指定的默认值，也就是语句中的 0000-00-00 00:00:00，但是很奇怪在本地就可以，为什么线上服务器就不行了？
后来经过查询文档（文档地址）发现，其实从5.6.17这个版本就默认设置了不允许插入 0 日期了，术语是 NO_ZERO_IN_DATE  NO_ZERO_DATE

## 解决方案
如果一定要设置为 0 日期的话，也是可以的，找到mysql的配置文件，在修改sql-mode,然后重启数据库服务
```
[mysqld]
#set the SQL mode to strict
#sql-mode="modes..." 
sql-mode = "STRICT_TRANS_TABLES,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"
```
查看sql-mode设置值的命令
```
SHOW VARIABLES LIKE 'sql_mode';
```
## 为什么
知道如何解决，但是我们也要想想为什么官网要这么设置，我个人理解如下：其实我们都知道 timestamps的范围是从 1970-01-01 00:00:01 到 2038-01-19 03:14:07，而数据库在发展的过程中 官网应该认为存储0日期是非常不正常的事情（或者存储0要花销更多的资源）



sql_mode常用值
ONLY_FULL_GROUP_BY：对于GROUP BY聚合操作，如果在SELECT中的列，没有在GROUP BY中出现，那么这个SQL是不合法的，因为列不在GROUP BY从句中



NO_AUTO_VALUE_ON_ZERO：该值影响自增长列的插入。默认设置下，插入0或NULL代表生成下一个自增长值。如果用户 希望插入的值为0，而该列又是自增长的，那么这个选项就有用了。



STRICT_TRANS_TABLES：在该模式下，如果一个值不能插入到一个事务表中，则中断当前的操作，对非事务表不做限制



NO_ZERO_IN_DATE：在严格模式下，不允许日期和月份为零



NO_ZERO_DATE：设置该值，mysql数据库不允许插入零日期，插入零日期会抛出错误而不是警告。



ERROR_FOR_DIVISION_BY_ZERO：在INSERT或UPDATE过程中，如果数据被零除，则产生错误而非警告。如 果未给出该模式，那么数据被零除时MySQL返回NULL



NO_AUTO_CREATE_USER：禁止GRANT创建密码为空的用户



NO_ENGINE_SUBSTITUTION：如果需要的存储引擎被禁用或未编译，那么抛出错误。不设置此值时，用默认的存储引擎替代，并抛出一个异常



PIPES_AS_CONCAT：将"||"视为字符串的连接操作符而非或运算符，这和Oracle数据库是一样的，也和字符串的拼接函数Concat相类似



ANSI_QUOTES：启用ANSI_QUOTES后，不能用双引号来引用字符串，因为它被解释为识别符
