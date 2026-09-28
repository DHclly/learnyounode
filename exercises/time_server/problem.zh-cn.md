创建一个名为 `time-server.js` 的文件。

编写一个 **TCP 时间服务器**！

你的服务器应该监听程序的第一个参数所提供的端口上的 TCP 连接。对每个连接，你必须按以下格式写入当前日期和 24 小时制时间：

```
"YYYY-MM-DD hh:mm"
```

后面再跟一个**换行符**。月、日、小时和分钟都必须*补零*到 2 位整数。例如：

```
"2013-07-06 17:42"
```

发送完这个字符串后，关闭连接。

----------------------------------------------------------------------
## 提示

这道练习中，我们将创建一个原始 TCP 服务器。这里不涉及 HTTP，所以我们需要使用 Node 核心中具备所有基础网络功能的 `net` 模块。

`net` 模块有一个名为 `net.createServer()` 的方法，它接收一个函数。你需要传给 `net.createServer()` 的函数是一个连接监听器，它会被调用不止一次。你的服务器每收到一个连接就会再次调用这个监听器。这个监听器函数的签名是：

```js
function listener (socket) { /* ... */ }
```

`net.createServer()` 还会返回一个你的 `server` 实例。你必须调用 `server.listen(portNumber)` 来开始监听某个特定端口。

一个典型的 Node TCP 服务器看起来像这样：

```js
const net = require('net')
const server = net.createServer(function (socket) {
  // socket 处理逻辑
})
server.listen(8000)
```

记得使用作为第一个命令行参数提供给你的端口号。

`socket` 对象包含许多关于该连接的元数据，但它同时也是一个 Node 双工 Stream，也就是说它既可读也可写。对这道练习，我们只需要写入数据然后关闭 socket。

用 `socket.write(data)` 把数据写入 socket，用 `socket.end()` 关闭 socket。另外，`.end()` 方法也可以接收一个数据对象，所以你可以简化为：`socket.end(data)`。

`net` 模块的文档可以通过浏览器访问以下地址来查看：

  {rootdir:/docs-nodejs/net.html}

要创建日期，你需要基于 `new Date()` 对象自定义一个格式。会用到的这些方法有：

```js
date.getFullYear()
date.getMonth() // 从 0 开始
date.getDate() // 返回当月第几天
date.getHours()
date.getMinutes()
```

或者，如果你想大胆一点，可以使用 npm 的 `strftime` 包。`strftime(fmt, date)` 函数接收的日期格式与 unix 的 `date` 命令相同。你可以在以下地址了解更多关于 strftime 的信息：https://github.com/samsonjs/strftime

运行下面的命令来检查你的程序是否正确：

```sh
$ {appname} verify time-server.js
```
