创建一个名为 `http-collect.js` 的文件。

编写一个程序，向作为第一个命令行参数提供给你的 URL 发起一个 HTTP GET 请求。收集来自服务器的**所有**数据（不只是第一个 "data" 事件），然后向终端（标准输出 stdout）写入两行内容。

你写出的第一行应该只是一个整数，表示从服务器收到的字符数。第二行应该包含服务器发送的完整字符串。

----------------------------------------------------------------------
## 提示

这道题有两种解法：

**1)** 跨多个 "data" 事件收集数据，在打印输出之前把结果追加在一起。用 "end" 事件判断 stream 何时结束，此时你就可以写出输出。

**2)** 使用第三方包来屏蔽收集整个数据流的麻烦。有两个不同的包提供了解决这个问题的实用 API（很可能还有更多！）：`bl`（Buffer List）和 `concat-stream`；任选其一！

  <https://npmjs.com/bl>
  <https://npmjs.com/concat-stream>

要安装 Node 包，请使用 Node 包管理器 `npm`。只需输入：

```sh
$ npm install bl
```

它会把包的最新版本下载并安装到一个名为 `node_modules` 的子目录中。任何位于你主程序文件所在目录下这个子目录中的包，都可以用 `require` 语法加载，而不需要加上 './' 前缀：

```js
const bl = require('bl')
```

Node 会先在核心模块中查找，然后才在包所在的 `node_modules` 目录中查找。

如果你没有网络连接，只需创建一个 `node_modules` 目录，然后从 {appname} 的安装目录中把你要用的包的整个目录复制过去：

  {rootdir:/node_modules/bl}
  {rootdir:/node_modules/concat-stream}

`bl` 和 `concat-stream` 都可以让一个 stream *piped* 进去，然后它们会替你收集数据。当 stream 结束后，会带着数据触发一个回调函数：

```js
response.pipe(bl(function (err, data) { /* ... */ }))
// 或
response.pipe(concatStream(function (data) { /* ... */ }))
```

注意你可能需要用 `data.toString()` 把 Buffer 转换成字符串。

这两个模块的文档已经随 {appname} 安装在你的系统上，你可以通过浏览器访问以下地址来阅读它们：

  {rootdir:/docs/bl.html}
  {rootdir:/docs/concat-stream.html}

运行下面的命令来检查你的程序是否正确：

```sh
$ {appname} verify http-collect.js
```
