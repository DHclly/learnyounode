建立一個名為 `http-json-api-server.js` 的檔案。

撰寫一個 HTTP **伺服器**，當它收到發往路徑 '/api/parsetime' 的 GET 請求時，回應 JSON 資料。請預期這個請求會包含一個查詢字串，鍵為 'iso'，值為 ISO 格式的時間。

例如：

  /api/parsetime?iso=2013-08-10T12:10:15.474Z

JSON 回應應該只包含 'hour'、'minute' 和 'second' 屬性。例如：

```json
{
  "hour": 14,
  "minute": 23,
  "second": 15
}
```

再加上第二個端點，路徑為 '/api/unixtime'，它接受相同的查詢字串，但在 'unixtime' 屬性下回傳 UNIX 紀元時間（自 1970 年 1 月 1 日 00:00:00 UTC 起的毫秒數）。例如：

```json
{ "unixtime": 1376136615474 }
```

你的伺服器應該監聽程式第一個參數所提供的連接埠。

----------------------------------------------------------------------
## 提示

HTTP 伺服器的 `request` 物件有一個 `url` 屬性，你需要用它來為這兩個端點*"路由"*你的請求。

你可以使用 Node 核心的 'url' 模組來解析 URL 和查詢字串。`new URL(request.url)` 會解析 request.url 的內容，並給你一個帶有實用屬性的物件。

例如，在命令提示字元中輸入：

```sh
$ node -pe "new URL('/test?q=1', 'http://example.com')"
```

`url` 模組的文件可以透過瀏覽器開啟以下網址來閱讀：
  {rootdir:/docs-nodejs/url.html}

你的回應應該是 JSON 字串格式。更多資訊請參考 `JSON.stringify()`。

你也應該當個稱職的 Web 公民，正確設定 Content-Type：

```js
res.writeHead(200, { 'Content-Type': 'application/json' })
```

JavaScript 的 `Date` 物件可以以 ISO 格式印出日期，例如 `new Date().toISOString()`。如果你把字串傳進 `Date` 建構子，它也可以解析這種格式。`Date.getTime()` 同樣
會派上用場。

執行下面的命令來檢查你的程式是否正確：

```sh
$ {appname} verify http-json-api-server.js
```
