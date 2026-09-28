创建一个名为 `http-json-api-server.js` 的文件。

编写一个 HTTP **服务器**，当它收到发往路径 '/api/parsetime' 的 GET 请求时，返回 JSON 数据。请预期该请求包含一个查询字符串，其键为 'iso'，值为 ISO 格式的时间。

例如：

  /api/parsetime?iso=2013-08-10T12:10:15.474Z

JSON 响应应该只包含 'hour'、'minute' 和 'second' 属性。例如：

```json
{
  "hour": 14,
  "minute": 23,
  "second": 15
}
```

再添加一个路径为 '/api/unixtime' 的端点，它接受相同的查询字符串，但在 'unixtime' 属性下返回 UNIX 纪元时间（自 1970 年 1 月 1 日 00:00:00 UTC 起的毫秒数）。例如：

```json
{ "unixtime": 1376136615474 }
```

你的服务器应该监听程序的第一个参数所提供的端口。

----------------------------------------------------------------------
## 提示

HTTP 服务器的 `request` 对象有一个 `url` 属性，你需要用它来为这两个端点*"路由"*你的请求。

你可以使用 Node 核心的 'url' 模块来解析 URL 和查询字符串。`new URL(request.url)` 会解析 request.url 的内容，并给你一个带有实用属性的对象。

例如，在命令提示符下输入：

```sh
$ node -pe "new URL('/test?q=1', 'http://example.com')"
```

`url` 模块的文档可以通过浏览器访问以下地址来查看：
  {rootdir:/docs-nodejs/url.html}

你的响应应该是 JSON 字符串格式。更多信息请查看 `JSON.stringify()`。

你还应该做一个合格的 Web 公民，正确设置 Content-Type：

```js
res.writeHead(200, { 'Content-Type': 'application/json' })
```

JavaScript 的 `Date` 对象可以以 ISO 格式打印日期，例如 `new Date().toISOString()`。如果你把字符串传给 `Date` 构造函数，它也可以解析这种格式。`Date.getTime()` 同样
会很有用。

运行下面的命令来检查你的程序是否正确：

```sh
$ {appname} verify http-json-api-server.js
```
