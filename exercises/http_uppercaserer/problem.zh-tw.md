建立一個名為 `http-uppercaserer.js` 的檔案。

撰寫一個 HTTP **伺服器**，它只接收 POST 請求，把收到的 POST 內容字元轉換成大寫，並回應給客戶端。

你的伺服器應該監聽程式第一個參數所提供的連接埠。

----------------------------------------------------------------------
## 提示

雖然並不限制你使用 `request` 和 `response` 物件的串流能力，但如果使用它們會簡單得多。

npm 中有許多不同的套件，你可以在串流資料通過時用它來*"轉換"*資料。這道練習中，`through2-map` 套件提供了最簡單的 API。

`through2-map` 允許你只用一個函式就建立一個 *transform stream*，這個函式接收一塊資料並回傳一塊資料。它的設計運作方式很像 `Array#map()`，但針對的是串流：

```js
const map = require('through2-map')
inStream.pipe(map(function (chunk) {
  return chunk.toString().split('').reverse().join('')
})).pipe(outStream)
```

在上面的例子中，來自 `inStream` 的傳入資料被轉換成字串（如果它還不是的話），字元順序被反轉，結果被傳送到 `outStream`。所以我們做了一個資料塊字元反轉器！不過請記住，資料塊的大小是由上游決定的，對傳入的資料你幾乎無法控制。

要安裝 `through2-map`，請輸入：

```sh
$ npm install through2-map
```

如果你沒有網路連線，只要建立一個 `node_modules` 目錄，然後從 {appname} 的安裝目錄中把你要用的套件的整個目錄複製過去：

  {rootdir:/node_modules/through2-map}

through2-map 的文件已經隨 {appname} 安裝在你的系統上，你可以透過瀏覽器開啟以下網址來閱讀：

  {rootdir:/docs/through2-map.html}

執行下面的命令來檢查你的程式是否正確：

```sh
$ {appname} verify http-uppercaserer.js
```
