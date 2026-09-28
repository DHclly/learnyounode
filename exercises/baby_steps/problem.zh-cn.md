创建一个名为 `baby-steps.js` 的文件。

编写一个程序，接收一个或多个数字作为命令行参数，并在终端（标准输出 stdout）打印出这些数字的总和。

----------------------------------------------------------------------
## 提示

你可以通过全局对象 `process` 来访问命令行参数。`process` 对象有一个 `argv` 属性，它是一个包含完整命令行的数组，即 `process.argv`。

为了上手，先编写一个只包含以下内容的程序：

```js
console.log(process.argv)
```

用 `node baby-steps.js` 加上几个数字作为参数来运行它，例如：

```sh
$ node baby-steps.js 1 2 3
```

这时，输出会是一个类似这样的数组：

```js
['node', '/path/to/your/baby-steps.js', '1', '2', '3']
```

你需要考虑如何遍历这些数字参数，以便只输出它们的总和。`process.argv` 数组的第一个元素永远是 `'node'`，第二个元素永远是你的 `baby-steps.js` 文件的路径，所以你需要从第 3 个元素（下标 2）开始，把每一项累加到总和里，直到数组末尾。

另外要注意，`process.argv` 的所有元素都是字符串，你可能需要把它们*转换*成数字。你可以通过在属性前加上 `+`，或者把它传给 `Number()` 来实现。例如 `+process.argv[2]` 或 `Number(process.argv[2])`。

运行下面的命令来检查你的程序是否正确：

```sh
$ {appname} verify baby-steps.js
```

当你运行 `{appname} verify baby-steps.js` 时，{appname} 会向你的程序提供参数，所以你不需要自己提供。如果想在不验证的情况下测试程序，可以用 `{appname} run baby-steps.js` 来调用它。当你使用 `run` 时，你用的是 {appname} 为每个练习搭建的测试环境。
