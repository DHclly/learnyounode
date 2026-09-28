建立一個名為 `http-collect.js` 的檔案。

撰寫一個程式，對第一個命令列參數所提供給你的 URL 發起一個 HTTP GET 請求。收集伺服器回傳的**所有**資料（不只是第一個 "data" 事件），然後向終端機（標準輸出 stdout）寫出兩行內容。

你寫出的第一行應該只是一個整數，代表從伺服器收到的字元數。第二行應該包含伺服器送出的完整字串。

----------------------------------------------------------------------
## 提示

這個問題有兩種解法：

**1)** 跨多個 "data" 事件收集資料，在印出輸出之前先把結果附加在一起。用 "end" 事件判斷串流何時結束，此時你就可以寫出輸出。

**2)** 使用第三方套件來擋掉收集整個資料流的麻煩。有兩個不同的套件提供了實用的 API 來解決這個問題（很可能還有更多！）：`bl`（Buffer List）和 `concat-stream`；任選一個！

  <https://npmjs.com/bl>
  <https://npmjs.com/concat-stream>

要安裝 Node 套件，請使用 Node 套件管理程式 `npm`。只要輸入：

```sh
$ npm install bl
```

它會把套件的最新版本下載並安裝到名為 `node_modules` 的子目錄中。任何位於你主程式檔案所在目錄下這個子目錄中的套件，都可以用 `require` 語法載入，而不需要加上 './' 前綴：

```js
const bl = require('bl')
```

Node 會先在核心模組中尋找，然後才在套件所在的 `node_modules` 目錄中尋找。

如果你沒有網路連線，只要建立一個 `node_modules` 目錄，然後從 {appname} 的安裝目錄中把你要用的套件的整個目錄複製過去：

  {rootdir:/node_modules/bl}
  {rootdir:/node_modules/concat-stream}

`bl` 和 `concat-stream` 都能讓一個串流 *piped* 進去，然後它們會替你收集資料。串流結束後，會帶著資料觸發一個回呼函式：

```js
response.pipe(bl(function (err, data) { /* ... */ }))
// 或
response.pipe(concatStream(function (data) { /* ... */ }))
```

注意你可能需要用 `data.toString()` 把 Buffer 轉換成字串。

這兩個模組的文件已經隨 {appname} 安裝在你的系統上，你可以透過瀏覽器開啟以下網址來閱讀它們：

  {rootdir:/docs/bl.html}
  {rootdir:/docs/concat-stream.html}

執行下面的命令來檢查你的程式是否正確：

```sh
$ {appname} verify http-collect.js
```
