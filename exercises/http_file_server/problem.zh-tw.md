建立一個名為 `http-file-server.js` 的檔案。

撰寫一個 HTTP **伺服器**，對它收到的每個請求都回應同一個文字檔。

你的伺服器應該監聽程式第一個參數所提供的連接埠。

程式的第二個命令列參數會提供要回應的檔案位置。你**必須**使用 `fs.createReadStream()` 方法把檔案內容以串流方式送到回應中。

----------------------------------------------------------------------
## 提示

因為這道練習需要建立一個 HTTP 伺服器，而不是一般的 TCP 伺服器，所以我們應該使用 Node 核心的 `http` 模組。就像 `net` 模組一樣，`http` 也有一個名為 `http.createServer()` 的方法，但它建立的是能用 HTTP 溝通的伺服器。

`http.createServer()` 接收一個回呼函式，伺服器每收到一個連線就會呼叫它一次。這個回呼函式的簽名是：

```js
function callback (request, response) { /* ... */ }
```

其中這兩個參數是分別代表 HTTP 請求和該請求對應回應的物件。`request` 用來取得屬性，例如請求中的 header 和 query-string，而 `response` 用來傳送資料給客戶端，包括 header 和 body。

`request` 和 `response` 也都是 Node 串流！這代表如果你的使用情境適合，你可以用串流抽象來收發資料。

`http.createServer()` 也會回傳一個 `server` 實例。你必須呼叫 `server.listen(portNumber)` 來開始監聽某個特定連接埠。

一個典型的 Node HTTP 伺服器看起來像這樣：

```js
const http = require('http')
const server = http.createServer(function (req, res) {
  // 處理請求的邏輯...
})
server.listen(8000)
```

`http` 模組的文件可以透過瀏覽器開啟以下網址來閱讀：
  {rootdir:/docs-nodejs/http.html}

`fs` 核心模組也有一些針對檔案的串流 API。你需要使用 `fs.createReadStream()` 方法，為你作為命令列參數取得的檔案建立一個串流。這個方法會回傳一個串流物件，你可以用 `src.pipe(dst)` 把資料從 `src` 串流管線到 `dst` 串流。這樣就能把檔案系統串流和 HTTP 回應串流連接起來。

執行下面的命令來檢查你的程式是否正確：

```sh
$ {appname} verify http-file-server.js
```
