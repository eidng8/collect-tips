[TOC]


[GitHub]: http://github.com/ (GitHub 官方)
[nodejs]: http://nodejs.org/ (nodejs 官方)
[grunt]: http://gruntjs.com/ (Grunt 官方)
[angular]: https://angularjs.org/ (AngularJS 官方)
[ionic]: http://ionicframework.com/ (Ionic Official Site)
[cordova]: https://cordova.apache.org/ (Apache Cordova Official Site)


## [Node.js][nodejs]

這個不解釋，做前端的都知道，有些做後端的也都知道。

由於官方的服務器全在中國大陸以外，所以在大陸使用會比較慢，而且不太穩定。目前在中國大陸地區可以使用[國內鏡像](http://npm.taobao.org/)。該站點內有使用說明，一般建議使用`cnpm`。

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

運行完以上命令後，就可以使用`cnpm`命令來取代`npm`命令了。

在使用了一段時間的cnpm後，發現其雖好用，但會新開一個自己的緩存。於是便直接用回npm了：

```bash
npm config -g set registry https://registry.npm.taobao.org
```

### `mirror-config-china`

如果不想使用`cnpm`，可以安裝`mirror-config-china`直接將所有相關東西改成國內鏡像。


## [Grunt][grunt]

[Grunt][grunt]是一個基於[Node.js][nodejs]的任務執行工具，在功能上類似於 Apache Ant。安裝方法如下：

- 在完成[Node.js][nodejs]及[GitHub客戶端][github]安裝後，在Windows開始菜單中找到`Git Shell`並運行。運行後會打開一個新的命令行窗口。
- 在`Git Shell`的命令行窗口中
  ```bash
  npm install -g grunt-cli
  ```


## [AngularJS][angular]

開發頁面級應用的JavaScript框架。它並不是DOM操作器，也不是設計工具。[AngularJS][angular]提供了直接在瀏覽器頁面開發應用的途徑。


### 教程

#### 線上

##### 官方

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

多端應用開發框架，能同時用於開發移動及桌面應用。基於[AngularJS][angular]和[Cordova][cordova]。


### 教程

#### 線上

##### 官方

http://learn.ionicframework.com/

##### 第三方

https://ccoenraets.github.io/ionic-tutorial/
https://thinkster.io/ionic-framework-tutorial/
http://coenraets.org/blog/2014/10/ionic-tutorial-and-sample-application/
https://www.airpair.com/ionic-framework/posts/ionic-socketio-chat-application-tutorial


#### PDF

https://ma.ellak.gr/documents/2014/10/ionic-framework.pdf
http://manning.com/wilken/IonicinA_MEAP_ch01.pdf
