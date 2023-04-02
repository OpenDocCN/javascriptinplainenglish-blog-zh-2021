# 用 JavaScript 剪贴板 API 创建一个复制按钮

> 原文：<https://javascript.plainenglish.io/javascript-creating-a-copy-button-with-the-clipboard-api-41bab347e601?source=collection_archive---------3----------------------->

![](img/c0daad47e3019332c326f0942f181121.png)

A West Oakland California Poppy

我喜欢这个在互联网上流行的新功能——不再需要点击和拖动来从网上复制内容。点击一个按钮，数据就神奇地出现在你的剪贴板上，你可以随心所欲地粘贴它。最棒的是，大多数现代浏览器都支持这一功能。那么如何实现呢？

很简单:

*   创建按钮
*   设置一个`onclick`监听器
*   在事件监听器中使用剪贴板 API

# 履行

HTML:

```
<button id='copy'>copy</button>
<textarea id='data'>un bel di vedremo</textarea>
```

JavaScript:

```
const btn_copy = document.getElementById('copy')
const txt_data = document.getElementById('data')copy.onclick = () => {
  const value = txt_data.value
  navigator.clipboard.writeText(value)
}
```

`writeText`返回一个承诺，该承诺在数据成功复制到剪贴板时解决，或者在写入失败时拒绝。对于这个例子，我们忽略这个承诺，但是如果您将大量数据复制到剪贴板，您应该让脚本等待这个写操作解决:

```
copy.onclick= async () => {
  const value = p_data.value
  await navigator.clipboard.writeText(value)
}
```

*你可以在这里* *查看一个活生生的例子* [*。*](https://jsbin.com/zefojixuya/edit?html,js,output)

# 但是它是如何工作的呢？

Clipboard API 允许 JavsScript 访问用户的剪贴板。剪贴板是您复制、剪切和粘贴所有数据的地方。您的系统允许您的浏览器访问这些数据，反过来，在某些条件下，浏览器允许您访问网站:

对剪贴板的读写访问必须由用户通过用户驱动的事件来触发，例如点击按钮、快捷键等。没有用户的互动，网站不能拷贝或粘贴。

写入权限会自动授予用户当前所在的网站。不专注的网站，其他的标签页，不能随便把东西复制到你的剪贴板上。

网站需要通过权限 API 请求读取权限。网站不会在没有问你的情况下阅读你复制的内容。

# 那么`document.execCommand`呢？

还可以使用`document.execCommand`读写剪贴板。然而，它被 FireFox 不推荐使用，而且不像 Clipboard API，它似乎没有官方的 web 标准来支持这个特定的目的。为了获得最好的浏览器支持和向前兼容性，我会使用剪贴板 API。更不用说，剪贴板 API 使用起来更容易、更安全、更干净。最好的是剪贴板 API 返回一个比布尔型`execCommand`返回更容易处理和链接的承诺。

# 逮到你了

当使用`writeText`时，数据被自动编码为 UTF-8，这对于大多数用例来说应该没问题，但是您可以使用`write([data])`手动设置编码。其中`data`是一个`ClipboardItem`实例。此项可以有任何文本或数据编码。例如，如果您只想复制中文文本进行翻译:`new ClipboardItem({'text/plain;charset=big5': text})`。

没有用户事件，您无法访问剪贴板 API。例如，如果您的网站运行生成长格式翻译的作业，您不能在该作业结束时将数据写入用户的剪贴板。用户必须触发一个事件，比如一次点击，这将授予你对剪贴板的写访问权。

**来源:**

[](https://jsbin.com/zefojixuya/edit?html,js,output) [## JS Bin

### 适用于 HTML、CSS 和 JavaScript 以及一系列处理器的实时 pastebin，包括 SCSS、CoffeeScript、Jade 等等...

jsbin.com](https://jsbin.com/zefojixuya/edit?html,js,output)  [## 剪贴板 API 和事件

### 本节是非规范性的。该规范定义了系统剪贴板如何向 web 应用程序公开…

www.w3.org](https://www.w3.org/TR/clipboard-apis/#async-clipboard-api)  [## Clipboard.writeText()

### 接口的属性将指定的文本字符串写入系统剪贴板。可以使用以下任一方式回读文本…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard/writeText)  [## Clipboard.write()

### 方法将图像等任意数据写入剪贴板。这可以用来实现剪切和复制…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard/write) [](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API) [## 剪贴板 API

### 剪贴板 API 提供了响应剪贴板命令(剪切、复制和粘贴)以及…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API) [](https://webcheatsheet.com/html/character_sets_list.php) [## 字符集列表

### 字符集列表

字符集 Listwebcheatsheet.com](https://webcheatsheet.com/html/character_sets_list.php) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)