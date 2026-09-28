创建一个名为 `http-client.js` 的文件。

编写一个程序，向作为第一个命令行参数提供给你的 URL 发起一个 HTTP GET 请求。把响应中**每一个** "data" 事件得到的字符串内容，在终端（标准输出 stdout）上打印成新的一行。

----------------------------------------------------------------------
## 提示

在这个练习中，你需要使用 `http` 核心模块。

`http` 模块的文档可以通过浏览器访问以下地址来查看：
  {rootdir:/docs-nodejs/http.html}

`http.get()` 方法是发起简单 GET 请求的快捷方式，用它来简化你的解答。`http.get()` 的第一个参数可以是你想要 GET 的 URL；第二个参数传入一个回调函数。

与其他回调函数不同，这个回调函数具有这样的签名：

```js
function callback (response) { /* ... */ }
```

其中 `response` 对象是一个 Node 的 **Stream** 对象。你可以把 Node Stream 当作会发出事件的对象。最需要关注的三个事件是："data"、"error" 和 "end"。你可以像这样监听一个事件：

```js
response.on('data', function (data) { /* ... */ })
```

"data" 事件会在有一块数据可供处理时被触发。数据块的大小取决于底层的数据源。

你从 `http.get()` 得到的 `response` 对象 / Stream 还有一个 `setEncoding()` 方法。如果你用 "utf8" 调用这个方法，"data" 事件将会发出字符串，而不是标准的 Node `Buffer` 对象——那种你必须显式转换成字符串的对象。

运行下面的命令来检查你的程序是否正确：

```sh
$ {appname} verify http-client.js
```
