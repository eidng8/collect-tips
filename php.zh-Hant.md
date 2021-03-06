[TOC]


[php]: http://php.net/ (PHP 官網)
[composer]:https://getcomposer.org/download (Composer 官網)



## PEAR
This is how you get it:
```text
http://pear.php.net/manual/en/installation.getting.php
```

## [Composer](composer)
[Composer](composer)是[PHP](php)的管理工具。Windows下可以使用[安裝包](https://getcomposer.org/Composer-Setup.exe "Windows安裝包")進行安裝，並且自動更新`PATH`環境變量。由於官方的服務器全在中國大陸以外，所以在大陸使用會比較慢，而且不太穩定。[阿里雲鏡像站](https://mirrors.aliyun.com/composer/composer.phar)上有PHAR版本。

- [阿里雲鏡像站](https://developer.aliyun.com/composer)
  ```text
  https://mirrors.aliyun.com/composer/
  ```


## 編程

### `+` （加號）數組操作符

[官方文檔](https://www.php.net/manual/en/language.operators.array.php)上說的意思是：將第二個數組合併入第一個數組，但保留第一個數組的原有鍵值內容。

```php
$a = array("a" => "apple", "b" => "banana");
$b = array("a" => "pear", "b" => "strawberry", "c" => "cherry");
$c = $a + $b; // Union of $a and $b
// yields
// array(3) {
//   ["a"]=>
//   string(5) "apple"
//   ["b"]=>
//   string(6) "banana"
//   ["c"]=>
//   string(6) "cherry"
// }
```


### `curl_multi`

cURL庫提為鏈接重用提供了一種方便的用法。

這篇[文章](http://technosophos.com/2012/06/18/connection-sharing-curl-php-how-re-use-http-connections-knock-70-rest-network-time.html)作了詳細說明。

以下提供了一段示例代碼。*注意*：不要在實際產品中直接使用以下代碼片段，因為這裡並沒有處理multi句柄的關閉問題。實際使用中應該要把相關功能封裝至一個類中，並在解構函數中關閉multi句柄。

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
