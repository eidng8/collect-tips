[TOC]


[GitHub]: http://github.com/ (GitHub 官網)
[nodejs]: http://nodejs.org/ (nodejs 官網)
[grunt]: http://gruntjs.com/ (Grunt 官網)

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


## [Grunt][grunt]

[Grunt][grunt]是一個基於[Node.js][nodejs]的任務執行工具，在功能上類似於 Apache Ant。安裝方法如下：

- 在完成[Node.js][nodejs]及[GitHub客戶端][github]安裝後，在Windows開始菜單中找到`Git Shell`並運行。運行後會打開一個新的命令行窗口。
- 在`Git Shell`的命令行窗口中
  ```bash
  npm install -g grunt-cli
  ```
