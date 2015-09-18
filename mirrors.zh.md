[TOC]


## 国内主要镜像站

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
- 前端公共库CDN
  - http://www.freecdn.cn/
- Google Fonts 镜像
  - http://www.googlefonts.cn/
- Composer 中文网
  - http://packagist.phpcomposer.com
- Packagist 中国镜像站
  - http://packagist.cn


## Android SDK 镜像

主要有三种方法：

### 修改`hosts`文件

在`hosts`文件中把`dl.google.com`解释至任一镜像站的IP。

### 使用代理

打开`Android SDK Manager`，菜单`Tools`>`Options...`，在`HTTP Proxy Server`及`HTTP Proxy Port`里分别填写代理的域名及端口。小心是**域名**，也就是没有`http://`。

### 修改站点列表

打开`Android SDK Manager`，菜单`Tools`>`Manage Add-on Sites...`，把`Offical Add-on Sites`里的所有站点禁用，然后在`User Defined Sites`里逐一加入相应的镜像URL。也就是将`Offical Add-on Sites`里的所有的域名换成镜像的域名，加入到`User Defined Sites`里。
