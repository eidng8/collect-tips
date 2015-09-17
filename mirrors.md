[TOC]


## Public Mirrors

- 网易开源镜像站
  - http://mirrors.163.com/
- 淘宝 NPM 镜像
  - http://npm.taobao.org/
- Toran Proxy (Composer)
  - http://pkg.uselaravel.com/repo/packagist/
- 北京化工大学镜像服务器地址: http://mirrors.neusoft.edu.cn
  - IPv4: http://ubuntu.buct.edu.cn/ 端口：80
  - IPv4: http://ubuntu.buct.cn/ 端口：80
  - IPv6: http://ubuntu.buct6.edu.cn/ 端口：80
- 上海GDG镜像服务器地址:
  - http://sdk.gdgshanghai.com 端口：8000
- 电子科技大学开源镜像站：
  - mirrors.dormforce.net
- Composer 中文网
  - http://packagist.phpcomposer.com
- Packagist 中国镜像站
  - http://packagist.cn


## Android SDK Mirrors

One can use mirrors by:

### Change `hosts` file

Map `dl.google.com` to any mirrors' IP address in `hosts` file.

### Use Proxy

Open `Android SDK Manager`, choose from menu `Tools`>`Options...`. Fill in mirrors' domain and port number to `HTTP Proxy Server` and `HTTP Proxy Port` respectively. Be careful to use **domain**, that's the part without `http://`.

### Change Sites

Open `Android SDK Manager`, choose from menu `Tools`>`Manage Add-on Sites...`. Disable everything inside `Offical Add-on Sites` tab. Then add corresponding mirror URL in `User Defined Sites` tab. That's it, replace every URL in the `Offical Add-on Sites` tab with mirrors' domain, and then add to `User Defined Sites` tab.
