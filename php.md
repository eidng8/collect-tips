[TOC]


[php]: http://php.net/ (PHP Official Site)
[composer]:https://getcomposer.org/download (Composer Official Site)


## PEAR
This is how you get it:
```text
http://pear.php.net/manual/en/installation.getting.php
```

## [Composer](composer)
[Composer](composer) is a [PHP](php) dependency manager. There's a [windows installer](https://getcomposer.org/Composer-Setup.exe). Remember to update the `PATH` environment variable after installation. However, the official packagist can't be accessed from China mainland.

There are a few mirrors in China mainland:

- [Packagist 中国镜像站](http://pkg.phpcomposer.com/)
  ```text
  http://packagist.cn
  ```
- [Composer 中文网](http://www.phpcomposer.com/)
  ```text
  http://packagist.phpcomposer.com
  ```

There are configuration steps on these sits. It is suggested to use global configuration option. However, these mirrors seems not so stable either.

Recently found, a Japanese mirror, which seems more stable.
```text
http://pkg.uselaravel.com/repo/packagist/
```


## Programming Tips

### `curl_multi`

The cURL library provides an convinient way of reusing connection.

This great [article](http://technosophos.com/2012/06/18/connection-sharing-curl-php-how-re-use-http-connections-knock-70-rest-network-time.html) explains quite well.

And below is a shot of related code fragment. *REMEBER* that this code can *NOT* be used in reality, since it doesn't close the multi handle after use. A real use involves encapsulating the process in a class, and close the multi handle in destructor.

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