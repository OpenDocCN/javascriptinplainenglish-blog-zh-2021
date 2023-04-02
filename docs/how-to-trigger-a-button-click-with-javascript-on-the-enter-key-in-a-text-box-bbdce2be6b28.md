# 如何用 JavaScript 在文本框中的回车键上触发按钮点击？

> 原文：<https://javascript.plainenglish.io/how-to-trigger-a-button-click-with-javascript-on-the-enter-key-in-a-text-box-bbdce2be6b28?source=collection_archive---------8----------------------->

![](img/2b0406d535b5e8b33abe34c0b2579b60.png)

Photo by [Tawhidur R](https://unsplash.com/@abscondet?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果我们的网页上有一个文本框，我们可能希望在按下回车键时触发一次按钮点击。

在本文中，我们将研究如何用 JavaScript 在文本框中按下回车键时触发按钮点击。

# 使用点击方法

我们可以调用 HTML 元素节点对象可用的`click`方法，以编程方式单击元素。

例如，我们可以编写以下 HTML:

```
<input type="text" id="txtSearch"  />
<input type="button" id="btnSearch" value="Search" />
```

然后，我们可以编写以下 JavaScript 代码来检查 Enter 键的按下情况，并在之后触发按钮单击:

```
const txtSearchEl = document.getElementById('txtSearch')
const btnSearchEl = document.getElementById('btnSearch')txtSearchEl.addEventListener('keydown', (event) => {
  if (event.keyCode == 13) {
    btnSearchEl.click()
  }
})btnSearchEl.addEventListener('click', () => {
  console.log('search button clicked')
})
```

我们用`document.getElementById`得到 2 个输入。

然后我们调用`txtSearchEl`上的`addEventListener`，将`'keydown'`字符串作为第一个参数，为`keydown` 事件添加一个事件监听器。

接下来，我们传入一个回调函数作为事件触发时运行的第二个参数。

在回调中，我们检查`keyCode`属性，看它是否是 13。

如果是，则按回车键。

然后我们得到`btnSearchEl` HTML 元素节点对象，也就是文本框下面的按钮，在上面调用`click`。

`click`方法以编程方式触发点击。

接下来，我们向`btnSearchEl`元素节点对象添加一个 click 监听器，在按钮被单击时执行一些操作。

所以当调用`click`时，我们应该看到`'search button clicked'`被记录。

我们也可以检查`event.key`属性，而不是`event.keyCode`属性。

例如，我们可以写:

```
const txtSearchEl = document.getElementById('txtSearch')
const btnSearchEl = document.getElementById('btnSearch')txtSearchEl.addEventListener('keydown', (event) => {
  if (event.key === "Enter") {
    btnSearchEl.click()
  }
})btnSearchEl.addEventListener('click', () => {
  console.log('search button clicked')
})
```

`event.key`返回一个我们按下的键的名称的字符串，所以这比检查一个键码更直观。

# 结论

我们可以通过使用事件监听器观察`keydown`事件来触发按键后的按钮点击。

在事件监听器中，我们调用按钮元素对象上的`click`以编程方式触发点击。

我们可以在按钮元素上附加一个`click`事件监听器，当我们点击按钮时做一些事情。

*更多内容看* [***说白了***](http://plainenglish.io/)