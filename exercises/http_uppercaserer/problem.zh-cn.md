创建一个名为 `http-uppercaserer.js` 的文件。

编写一个 HTTP **服务器**，它只接收 POST 请求，把收到的 POST 请求体中的字符转换成大写，并返回给客户端。

你的服务器应该监听程序的第一个参数所提供的端口。

----------------------------------------------------------------------
## 提示

虽然并不限制你使用 `request` 和 `response` 对象的流式能力，但如果使用它们会简单得多。

npm 中有许多不同的包，你可以在 stream 数据通过时用它来*"转换"*数据。这道练习中，`through2-map` 包提供了最简单的 API。

`through2-map` 允许你只用一个函数就创建一个 *transform stream*，这个函数接收一块数据并返回一块数据。它的设计工作方式很像 `Array#map()`，但针对的是 stream：

```js
const map = require('through2-map')
inStream.pipe(map(function (chunk) {
  return chunk.toString().split('').reverse().join('')
})).pipe(outStream)
```

在上面的例子中，来自 `inStream` 的传入数据被转换成字符串（如果它还不是的话），字符被反转，结果被传送到 `outStream`。所以我们做了一个数据块字符反转器！不过请记住，数据块的大小是由上游决定的，对传入的数据你几乎无法控制。

要安装 `through2-map`，请输入：

```sh
$ npm install through2-map
```

如果你没有网络连接，只需创建一个 `node_modules` 目录，然后从 {appname} 的安装目录中把你要用的模块的整个目录复制过去：

  {rootdir:/node_modules/through2-map}

through2-map 的文档已经随 {appname} 安装在你的系统上，你可以通过浏览器访问以下地址来阅读：

  {rootdir:/docs/through2-map.html}

运行下面的命令来检查你的程序是否正确：

```sh
$ {appname} verify http-uppercaserer.js
```
