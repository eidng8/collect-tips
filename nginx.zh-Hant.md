# Dealing with HTTP 502

## General
- Is up-stream working (not died)?
- Is socket is accesible?

Others also said:
- 查看当前的PHP FastCGI进程数是否够用：
  ```bash
  netstat -anpo | grep "php-cgi" | wc -l
  ```
  如果实际使用的“FastCGI进程数”接近预设的“FastCGI进程数”，那么，说明“FastCGI进程数”不够用，需要增大。
- 部分PHP程序的执行时间超过了Nginx的等待时间，可以适当增加nginx.conf配置文件中FastCGI的timeout时间，例如：
  ```ini
  http
  {
    fastcgi_connect_timeout 300;
    fastcgi_send_timeout 300;
    fastcgi_read_timeout 300;
  }
  ```
- php.ini中memory_limit设低了会出错，修改了php.ini的memory_limit为64M，重启nginx，发现好了，原来是PHP的内存不足了。
- 一、max-children和max-requests

一台服务器上运行着nginx php(fpm) xcache，访问量日均 300W pv左右

最近经常会出现这样的情况： php页面打开很慢，cpu使用率突然降至很低，系统负载突然升至很高，查看网卡的流量，也会发现突然降到了很低。这种情况只持续数秒钟就恢复了

检查php-fpm的日志文件发现了一些线索

Sep 30 08:32:23.289973 [NOTICE] fpm_unix_init_main(), line 271: getrlimit(nofile): max:51200, cur:51200
Sep 30 08:32:23.290212 [NOTICE] fpm_sockets_init_main(), line 371: using inherited socket fd=10, “127.0.0.1:9000″
Sep 30 08:32:23.290342 [NOTICE] fpm_event_init_main(), line 109: libevent: using epoll
Sep 30 08:32:23.296426 [NOTICE] fpm_init(), line 47: fpm is running, pid 30587

在这几句的前面，是1000多行的关闭children和开启children的日志

原来，php-fpm有一个参数 max_requests，该参数指明了，每个children最多处理多少个请求后便会被关闭，默认的设置是500。因为php是把请求轮询给每个children，在大流量下，每个childre到达max_requests所用的时间都差不多，这样就造成所有的children基本上在同一时间被关闭。

在这期间，nginx无法将php文件转交给php-fpm处理，所以cpu会降至很低(不用处理php，更不用执行sql)，而负载会升至很高(关闭和开启children、nginx等待php-fpm)，网卡流量也降至很低(nginx无法生成数据传输给客户端)

解决问题很简单，增加children的数量，并且将 max_requests 设置未 0 或者一个比较大的值：

打开 /usr/local/php/etc/php-fpm.conf

调大以下两个参数(根据服务器实际情况，过大也不行）

<value name=”max_children”>5120</value>
<value name=”max_requests”>600</value>

然后重启php-fpm。

二、增加缓冲区容量大小

将nginx的error log打开，发现“pstream sent too big header while reading response header from upstream”这样的错误提示。查阅了一下资料，大意是nginx缓冲区有一个bug造成的,我们网站的页面消耗占用缓冲区可能过大。参考老外写的修改办法增加了缓冲区容量大小设置，502问题彻底解决。后来系统管理员又对参数做了调整只保留了2个设置参数：client head buffer，fastcgi buffer size。

三、request_terminate_timeout

如果主要是在一些post或者数据库操作的时候出现502这种情况，而不是在静态页面操作中常见，那么可以查看一下php-fpm.conf设置中的一项：

request_terminate_timeout

这个值是max_execution_time，就是fast-cgi的执行脚本时间。

0s

0s为关闭，就是无限执行下去。（当时装的时候没仔细看就改了一个数字）

发现，问题解决了，执行很长时间也不会出错了。

优化fastcgi中，还可以改改这个值5s 看看效果。

php-cgi进程数不够用、php执行时间长、或者是php-cgi进程死掉，都会出现502错误。


## 優化

- 這篇[博文](http://blog.martinfjordvald.com/2011/04/optimizing-nginx-for-high-traffic-loads/)甚好。

- 錯誤(24: Too many open files)可能說明要增加文件打開閥值（ulimit or worker_rlimit_nofile）。
