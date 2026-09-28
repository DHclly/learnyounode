建立一個名為 `time-server.js` 的檔案。

撰寫一個 **TCP 時間伺服器**！

你的伺服器應該監聽程式第一個參數所提供的連接埠上的 TCP 連線。對每個連線，你都必須按以下格式寫入目前的日期和 24 小時制時間：

```
"YYYY-MM-DD hh:mm"
```

後面再接著一個**換行字元**。月、日、小時和分鐘都必須*補零*到 2 位整數。例如：

```
"2013-07-06 17:42"
```

送出這個字串後，關閉連線。

----------------------------------------------------------------------
## 提示

這道練習中，我們將建立一個原始 TCP 伺服器。這裡不涉及 HTTP，所以我們需要使用 Node 核心中具備所有基礎網路功能的 `net` 模組。

`net` 模組有一個名為 `net.createServer()` 的方法，它接收一個函式。你需要傳給 `net.createServer()` 的函式是一個連線監聽器，它會被呼叫不止一次。你的伺服器每收到一個連線就會再次呼叫這個監聽器。這個監聽器函式的簽名是：

```js
function listener (socket) { /* ... */ }
```

`net.createServer()` 還會回傳一個你的 `server` 實例。你必須呼叫 `server.listen(portNumber)` 來開始監聽某個特定連接埠。

一個典型的 Node TCP 伺服器看起來像這樣：

```js
const net = require('net')
const server = net.createServer(function (socket) {
  // socket 處理邏輯
})
server.listen(8000)
```

記得使用作為第一個命令列參數提供給你的連接埠號。

`socket` 物件包含許多關於該連線的 meta-data，但它同時也是一個 Node 雙工串流（duplex Stream），也就是說它既可讀也可寫。對這道練習，我們只需要寫入資料然後關閉 socket。

用 `socket.write(data)` 把資料寫入 socket，用 `socket.end()` 關閉 socket。另外，`.end()` 方法也可以接收一個資料物件，所以你可以簡化為：`socket.end(data)`。

`net` 模組的文件可以透過瀏覽器開啟以下網址來閱讀：

  {rootdir:/docs-nodejs/net.html}

要建立日期，你需要基於 `new Date()` 物件自訂一個格式。會用到的這些方法有：

```js
date.getFullYear()
date.getMonth() // 從 0 開始
date.getDate() // 回傳當月第幾天
date.getHours()
date.getMinutes()
```

或者，如果你想大膽一點，可以使用 npm 的 `strftime` 套件。`strftime(fmt, date)` 函式接收的日期格式與 unix 的 `date` 命令相同。你可以在以下網址了解更多關於 strftime 的資訊：https://github.com/samsonjs/strftime

執行下面的命令來檢查你的程式是否正確：

```sh
$ {appname} verify time-server.js
```
