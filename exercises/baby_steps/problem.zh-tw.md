建立一個名為 `baby-steps.js` 的檔案。

撰寫一個程式，接收一個或多個數字作為命令列參數，並把這些數字的總和印到終端機（標準輸出 stdout）。

----------------------------------------------------------------------
## 提示

你可以透過全域物件 `process` 來存取命令列參數。`process` 物件有一個 `argv` 屬性，它是一個包含完整命令列的陣列，也就是 `process.argv`。

為了起步，請先撰寫一個只包含以下內容的程式：

```js
console.log(process.argv)
```

用 `node baby-steps.js` 並在後面加上幾個數字作為參數來執行它，例如：

```sh
$ node baby-steps.js 1 2 3
```

在這種情況下，輸出會是類似下面這樣的陣列：

```js
['node', '/path/to/your/baby-steps.js', '1', '2', '3']
```

你需要思考如何用迴圈逐一處理這些數字參數，以便只輸出它們的總和。`process.argv` 陣列的第一個元素永遠是 `'node'`，第二個元素永遠是你的 `baby-steps.js` 檔案的路徑，所以你必須從第 3 個元素（索引 2）開始，把每一項加進總和，直到陣列結束。

另外要注意，`process.argv` 的所有元素都是字串，你可能需要將它們*轉換*成數字。你可以用兩種方式做到：在屬性前面加上 `+`，或是把它傳給 `Number()`。例如 `+process.argv[2]` 或 `Number(process.argv[2])`。

執行下面的命令來檢查你的程式是否正確：

```sh
$ {appname} verify baby-steps.js
```

當你執行 `{appname} verify baby-steps.js` 時，{appname} 會為你的程式提供參數，所以你不需要自己提供。如果想在不驗證的情況下測試程式，可以用 `{appname} run baby-steps.js` 來執行它。當你使用 `run` 時，你用的是 {appname} 為每個練習架設的測試環境。
