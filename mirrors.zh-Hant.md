[TOC]


## 國內主要鏡像站

- 網易開源鏡像站
  - http://mirrors.163.com/
- 淘寶 NPM 鏡像
  - http://npm.taobao.org/
- Toran Proxy (Composer)
  - http://pkg.uselaravel.com/repo/packagist/
- 北京化工大學鏡像服務器地址: http://mirrors.neusoft.edu.cn
  - IPv4: http://ubuntu.buct.edu.cn/ 端口：80
  - IPv4: http://ubuntu.buct.cn/ 端口：80
  - IPv6: http://ubuntu.buct6.edu.cn/ 端口：80
- 上海GDG鏡像服務器地址:
  - http://sdk.gdgshanghai.com 端口：8000
- 電子科技大學開源鏡像站：
  - mirrors.dormforce.net
- 前端公共库CDN
  - http://www.freecdn.cn/
- Google Fonts 镜像
  - http://www.googlefonts.cn/
- Packagist 中國鏡像站
  - http://packagist.cn
- Composer 中文網
  - http://packagist.phpcomposer.com


## Android SDK 鏡像

主要有三種方法：

### 修改`hosts`文件

在`hosts`文件中把`dl.google.com`解釋至任一鏡像站的IP。

### 使用代理

打開`Android SDK Manager`，菜單`Tools`>`Options...`，在`HTTP Proxy Server`及`HTTP Proxy Port`裡分別填寫代理的域名及端口。小心是**域名**，也就是沒有`http://`。

### 修改站點列表

打開`Android SDK Manager`，菜單`Tools`>`Manage Add-on Sites...`，把`Offical Add-on Sites`裡的所有站點禁用，然後在`User Defined Sites`裡逐一加入相應的鏡像URL。也就是將`Offical Add-on Sites`裡的所有的域名換成鏡像的域名，加入到`User Defined Sites`裡。
