1.php.ini文件位置查找：php71 -i | grep /php.ini 


2. 一般的文件上传,除非文件很小.就像一个5M的文件,很可能要超过一分钟才能上传完.

但在php中,默认的该页最久执行时间为 30 秒.就是说超过30秒,该脚本就停止执行.

这就导致出现 无法打开网页的情况.这时我们可以修改 max_execution_time

在php.ini里查找


```

max_execution_time

```

默认是30秒.改为

```
max_execution_time = 0
```

0表示没有限制

3. 修改 post_max_size 设定 POST 数据所允许的最大大小。此设定也影响到文件上传。

php默认的post_max_size 为2M.如果 POST 数据尺寸大于 post_max_size $_POST 和 $_FILES superglobals 便会为空.

查找 post_max_size .改为

```
post_max_size = 150M

```
--------------------- 
4. 很多人都会改了第二步.但上传文件时最大仍然为 8M.

为什么呢.我们还要改一个参数upload_max_filesize 表示所上传的文件的最大大小。

查找upload_max_filesize,默认为8M改为

```
upload_max_filesize = 100M

```
PS:post_max_size 大于 upload_max_filesize 为佳.
