创建一个名为 `http-file-server.js` 的文件。

编写一个 HTTP **服务器**，它对收到的每个请求都返回同一个文本文件。

你的服务器应该监听程序的第一个参数所提供的端口。

程序的第二个命令行参数会提供要返回的文件的位置。你**必须**使用 `fs.createReadStream()` 方法把文件内容以流的方式送到响应中。

----------------------------------------------------------------------
## 提示

因为这道练习需要创建一个 HTTP 服务器，而不是一个通用的 TCP 服务器，所以我们应该使用 Node 核心的 `http` 模块。和 `net` 模块一样，`http` 也有一个名为 `http.createServer()` 的方法，但它创建的是能够使用 HTTP 通信的服务器。

`http.createServer()` 接收一个回调函数，服务器每收到一个连接就会调用它一次。这个回调函数的签名是：

```js
function callback (request, response) { /* ... */ }
```

其中这两个参数是分别代表 HTTP 请求和该请求对应的响应的对象。`request` 用来读取属性，例如请求中的 header 和 query-string，而 `response` 用于向客户端发送数据，包括 header 和 body。

`request` 和 `response` 也都是 Node stream！这意味着，如果你的使用场景适合，你可以使用流式抽象来收发数据。

`http.createServer()` 还会返回一个 `server` 实例。你必须调用 `server.listen(portNumber)` 来开始监听某个特定端口。

一个典型的 Node HTTP 服务器看起来像这样：

```js
const http = require('http')
const server = http.createServer(function (req, res) {
  // 处理请求的逻辑...
})
server.listen(8000)
```

`http` 模块的文档可以通过浏览器访问以下地址来查看：
  {rootdir:/docs-nodejs/http.html}

`fs` 核心模块也有一些用于文件的流式 API。你需要使用 `fs.createReadStream()` 方法，为你作为命令行参数得到的文件创建一个 stream。该方法返回一个 stream 对象，你可以用 `src.pipe(dst)` 把数据从 `src` 流管道到 `dst` 流。这样，你就能把一个文件系统流和一个 HTTP 响应流连接起来。

运行下面的命令来检查你的程序是否正确：

```sh
$ {appname} verify http-file-server.js
```
