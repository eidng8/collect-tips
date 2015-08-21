[TOC]


[GitHub]: http://github.com/ (GitHub 官网)
[nodejs]: http://nodejs.org/ (nodejs 官网)
[grunt]: http://gruntjs.com/ (Grunt 官网)
[angular]: https://angularjs.org/ (AngularJS 官网)
[ionic]: http://ionicframework.com/ (Ionic Official Site)
[cordova]: https://cordova.apache.org/ (Apache Cordova Official Site)


## [Node.js][nodejs]

这个不解释，做前端的都知道，有些做后端的也都知道。

由于官方的服务器全在中国大陆以外，所以在大陆使用会比较慢，而且不太稳定。目前在中国大陆地区可以使用[国内镜像](http://npm.taobao.org/)。该站点内有使用说明，一般建议使用`cnpm`。

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

运行完以上命令后，就可以使用`cnpm`命令来取代`npm`命令了。

在使用了一段时间的cnpm后，发现其虽好用，但会新开一个自己的缓存。于是便直接用回npm了：

```bash
npm config -g set registry https://registry.npm.taobao.org
```


## [Grunt][grunt]

[Grunt][grunt]是一个基于[Node.js][nodejs]的任务执行工具，在功能上类似于 Apache Ant。安装方法如下：

- 在完成[Node.js][nodejs]及[GitHub客户端][github]安装后，在Windows开始菜单中找到`Git Shell`并运行。运行后会打开一个新的命令行窗口。
- 在`Git Shell`的命令行窗口中
  ```bash
  npm install -g grunt-cli
  ```


## [AngularJS][angular]

开发页面级应用的JavaScript框架。它并不是DOM操作器，也不是设计工具。[AngularJS][angular]提供了直接在浏览器页面开发应用的途径。


### 教程

#### 在线

##### 官网

https://docs.angularjs.org/tutorial/

##### 第三方
http://www.w3schools.com/angular/
http://www.toptal.com/angular-js/a-step-by-step-guide-to-your-first-angularjs-app
https://www.codecademy.com/courses/learn-angularjs
https://thinkster.io/a-better-way-to-learn-angularjs/
http://www.tutorialspoint.com/angularjs/


#### PDF

http://www.tutorialspoint.com/angularjs/angularjs_tutorial.pdf
http://fastandfluid.com/publicdownloads/AngularJSIn60MinutesIsh_DanWahlin_May2013.pdf


## [Ionic][ionic]

多端应用开发框架，能同时用于开发移动及桌面应用。基于[AngularJS][angular]和[Cordova][cordova]。


### 教程

#### 在线

##### 官网

http://learn.ionicframework.com/

##### 第三方

https://ccoenraets.github.io/ionic-tutorial/
https://thinkster.io/ionic-framework-tutorial/
http://coenraets.org/blog/2014/10/ionic-tutorial-and-sample-application/
https://www.airpair.com/ionic-framework/posts/ionic-socketio-chat-application-tutorial


#### PDF

https://ma.ellak.gr/documents/2014/10/ionic-framework.pdf
http://manning.com/wilken/IonicinA_MEAP_ch01.pdf
