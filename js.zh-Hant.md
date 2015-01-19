### [Node.js][nodejs]
用于安装开发中使用到的工具。由于官方的服务器全在中国大陆以外，所以在大陆使用会比较慢，而且不太稳定。目前在中国大陆地区可以使用[国内镜像](http://npm.taobao.org/)。该站点内有使用说明，一般建议使用`cnpm`。
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
运行完以上命令后，就可以使用`cnpm`命令来取代`npm`命令了。


#### [Grunt][grunt]
[Grunt][grunt]是一个基于[Node.js][nodejs]的任务执行工具，在功能上类似于 Apache Ant。本项目中除[PHP][php]外的所有代码都由 [Grunt][grunt]进行处理。安装方法如下：

- 在完成[Node.js][nodejs]及[GitHub客户端][github]安装后，在Windows开始菜单中找到`Git Shell`并运行。运行后会打开一个新的命令行窗口。
- 在`Git Shell`的命令行窗口中，进入本项目的`workplace`目录（如：`cd d:\some\dir\eclipse\workplace`，在该目录下包含有`package.json`）。运行
  ```bash
  npm install -g grunt-cli
  npm install
  ```
  如要使用`cnpm`，只需将`npm`换成`cnpm`
  ```bash
  cnpm install -g grunt-cli
  cnpm install
  ```