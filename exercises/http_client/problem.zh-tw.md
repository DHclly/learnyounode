建立一個名為 `http-client.js` 的檔案。

撰寫一個程式，對第一個命令列參數所提供給你的 URL 發起一個 HTTP GET 請求。把回應中**每個** "data" 事件得到的字串內容，在終端機（標準輸出 stdout）上印成新的一行。

----------------------------------------------------------------------
## 提示

在這個練習中，你需要使用 `http` 核心模組。

`http` 模組的文件可以透過瀏覽器開啟以下網址來閱讀：
  {rootdir:/docs-nodejs/http.html}

`http.get()` 方法是發起簡單 GET 請求的快捷方式，用它來簡化你的解法。`http.get()` 的第一個參數可以是你想要 GET 的 URL；第二個參數傳入一個回呼函式。

和其他回呼函式不同，這個回呼函式有這樣的簽名：

```js
function callback (response) { /* ... */ }
```

其中 `response` 物件是一個 Node 的 **Stream** 物件。你可以把 Node Stream 當成會發出事件的物件。最需要關注的三個事件是："data"、"error" 和 "end"。你可以像這樣監聽一個事件：

```js
response.on('data', function (data) { /* ... */ })
```

"data" 事件會在有一塊資料可供處理時被發出。這塊資料的大小取決於底層的資料來源。

你從 `http.get()` 取得的 `response` 物件 / Stream 也有一個 `setEncoding()` 方法。如果你用 "utf8" 呼叫這個方法，"data" 事件將會發出字串，而不是標準的 Node `Buffer` 物件——那種你必須顯式轉換成字串的物件。

執行下面的命令來檢查你的程式是否正確：

```sh
$ {appname} verify http-client.js
```
