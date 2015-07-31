# Dealing with HTTP 502

## General
- Is up-stream working (not died)?
- Is socket is accesible?

Others also said:
- 查看當前的PHP FastCGI進程數是否夠用：
  ```bash
  netstat -anpo | grep "php-cgi" | wc -l
  ```
  如果實際使用的「FastCGI進程數」接近預設的「FastCGI進程數」，那麼，說明「FastCGI進程數」不夠用，需要增大。
- 部分PHP程序的執行時間超過了Nginx的等待時間，可以適當增加nginx.conf配置文件中FastCGI的timeout時間，例如：
  ```ini
  http
  {
    fastcgi_connect_timeout 300;
    fastcgi_send_timeout 300;
    fastcgi_read_timeout 300;
  }
  ```
- php.ini中memory_limit設低了會出錯，修改了php.ini的memory_limit為64M，重啟nginx，發現好了，原來是PHP的內存不足了。
- 一、max-children和max-requests

一台服務器上運行著nginx php(fpm) xcache，訪問量日均 300W pv左右

最近經常會出現這樣的情況： php頁面打開很慢，cpu使用率突然降至很低，系統負載突然升至很高，查看網卡的流量，也會發現突然降到了很低。這種情況只持續數秒鐘就恢復了

檢查php-fpm的日誌文件發現了一些線索

Sep 30 08:32:23.289973 [NOTICE] fpm_unix_init_main(), line 271: getrlimit(nofile): max:51200, cur:51200
Sep 30 08:32:23.290212 [NOTICE] fpm_sockets_init_main(), line 371: using inherited socket fd=10, 「127.0.0.1:9000〞
Sep 30 08:32:23.290342 [NOTICE] fpm_event_init_main(), line 109: libevent: using epoll
Sep 30 08:32:23.296426 [NOTICE] fpm_init(), line 47: fpm is running, pid 30587

在這幾句的前面，是1000多行的關閉children和開啟children的日誌

原來，php-fpm有一個參數 max_requests，該參數指明了，每個children最多處理多少個請求後便會被關閉，默認的設置是500。因為php是把請求輪詢給每個children，在大流量下，每個childre到達max_requests所用的時間都差不多，這樣就造成所有的children基本上在同一時間被關閉。

在這期間，nginx無法將php文件轉交給php-fpm處理，所以cpu會降至很低(不用處理php，更不用執行sql)，而負載會升至很高(關閉和開啟children、nginx等待php-fpm)，網卡流量也降至很低(nginx無法生成數據傳輸給客戶端)

解決問題很簡單，增加children的數量，並且將 max_requests 設置未 0 或者一個比較大的值：

打開 /usr/local/php/etc/php-fpm.conf

調大以下兩個參數(根據服務器實際情況，過大也不行）

<value name=」max_children」>5120</value>
<value name=」max_requests」>600</value>

然後重啟php-fpm。

二、增加緩衝區容量大小

將nginx的error log打開，發現「pstream sent too big header while reading response header from upstream」這樣的錯誤提示。查閱了一下資料，大意是nginx緩衝區有一個bug造成的,我們網站的頁面消耗佔用緩衝區可能過大。參考老外寫的修改辦法增加了緩衝區容量大小設置，502問題徹底解決。後來系統管理員又對參數做了調整只保留了2個設置參數：client head buffer，fastcgi buffer size。

三、request_terminate_timeout

如果主要是在一些post或者數據庫操作的時候出現502這種情況，而不是在靜態頁面操作中常見，那麼可以查看一下php-fpm.conf設置中的一項：

request_terminate_timeout

這個值是max_execution_time，就是fast-cgi的執行腳本時間。

0s

0s為關閉，就是無限執行下去。（當時裝的時候沒仔細看就改了一個數字）

發現，問題解決了，執行很長時間也不會出錯了。

優化fastcgi中，還可以改改這個值5s 看看效果。

php-cgi進程數不夠用、php執行時間長、或者是php-cgi進程死掉，都會出現502錯誤。