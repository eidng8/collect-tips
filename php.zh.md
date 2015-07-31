[TOC]


[php]: http://php.net/ (PHP 官网)
[composer]:https://getcomposer.org/download (Composer 官网)



## PEAR
This is how you get it:
```text
http://pear.php.net/manual/en/installation.getting.php
```

## [Composer](composer)
[Composer](composer)是[PHP](php)的管理工具。Windows下可以使用[安装包](https://getcomposer.org/Composer-Setup.exe "Windows安装包")进行安装，并且自动更新`PATH`环境变量。由于官方的服务器全在中国大陆以外，所以在大陆使用会比较慢，而且不太稳定。

在中国大陆地区有一些：

- [Packagist 中国镜像站](http://pkg.phpcomposer.com/)
  ```text
  http://packagist.cn
  ```
- [Composer 中文网](http://www.phpcomposer.com/)
  ```text
  http://packagist.phpcomposer.com
  ```

这些站点内有使用说明，一般建议使用全局配置的方法。在使用了一段时间后发现，目前的中国镜像站十分不稳定。

最近发现了一个日本镜像，好像比较稳定：
```text
http://pkg.uselaravel.com/repo/packagist/
```


## 编程

### `curl_multi`

cURL库提为链接重用提供了一种方便的用法。

这篇[文章](http://technosophos.com/2012/06/18/connection-sharing-curl-php-how-re-use-http-connections-knock-70-rest-network-time.html)作了详细说明。

以下提供了一段示例代码。*注意*：不要在实际产品中直接使用以下代码片段，因为这里并没有处理multi句柄的关闭问题。实际使用中应该要把相关功能封装至一个类中，并在解构函数中关闭multi句柄。

```php
/**
 * Use curl_multi() to perform actual stuff, instead of curl_exec()
 * @param {resource} $curl The cURL handle returned from curl_init()
 * @param {array}    $opts cURL options
 * @return {boolean|string} Returns the content if using CURLOPT_RETURNTRANSFER,
 *  otherwise true
 */
function curlMultiExec($curl, $opts = null)
{
  static $multi = null;
  $ret = true;

  // Create a multi if necessary.
  if(empty($multi))
    $multi = curl_multi_init();

  if(is_array($opts))
    curl_setopt_array($curl, $opts);

  // Add the handle to be processed.
  curl_multi_add_handle($multi, $curl);

  // Do all the processing.
  $active = null;
  do{
    $ret = curl_multi_exec($multi, $active);
  }while($ret == CURLM_CALL_MULTI_PERFORM);

  while($active && $ret == CURLM_OK)
  {
    if(curl_multi_select($multi) != -1)
    {
      do{
        $mrc = curl_multi_exec($multi, $active);
      }while($mrc == CURLM_CALL_MULTI_PERFORM);
    }
  }

  if(!empty($opts[CURLOPT_RETURNTRANSFER]))
    $ret = curl_multi_getcontent($curl);

  // Remove the handle from the multi processor.
  curl_multi_remove_handle($multi, $curl);

  return $ret;
}
```