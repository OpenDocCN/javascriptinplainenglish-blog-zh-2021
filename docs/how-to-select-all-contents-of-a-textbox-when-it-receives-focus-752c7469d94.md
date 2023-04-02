# 当文本框获得焦点时，如何选择它的所有内容？

> 原文：<https://javascript.plainenglish.io/how-to-select-all-contents-of-a-textbox-when-it-receives-focus-752c7469d94?source=collection_archive---------8----------------------->

![](img/11f5801295b663f58629f8d7e7a5acab.png)

Photo by [Spikeball](https://unsplash.com/@spikeball?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在文本框获得焦点时选择它的所有内容。

在本文中，我们将研究如何在文本框获得焦点时选择它的所有内容。

# 当文本框获得焦点时，选择它的所有内容

我们可以通过监听`focus`事件来选择文本框接收焦点时的所有内容。

例如，我们可以编写以下 HTML:

```
<input type="text" value="test" />
```

和下面的 JavaScript 代码:

```
const input = document.querySelector('input')
input.addEventListener('focus', () => {
  input.select();
})input.addEventListener('mouseup', (e) => {
  e.preventDefault()
})
```

我们用`querySelector`得到输入。

然后我们用`'focus'`作为第一个参数调用`addEventListener`来监听焦点事件。

然后我们调用输入的`select`方法，当我们点击文本框时，选择输入中的所有文本。

此外，我们还添加了一个`mouseup`事件监听器，并调用`e.preventDefault`来停止它的默认操作，即取消选中单击。

# 使用 React 在文本输入中选择输入文本

我们可以用 React easily 做同样的事情。

例如，我们可以写:

```
import React from "react";export default function App() {
  return (
    <div>
      <input type="text" value="test" onFocus={(e) => e.target.select()} />
    </div>
  );
}
```

我们只是传入一个调用`e.target.select`的函数来选择输入中的所有文本作为`onFocus`属性的值。

`e.target`是输入元素，所以我们可以在上面调用`select`来选择所有文本。

# 结论

通过编写几行 JavaScript 代码，我们可以选择输入框中的所有文本。

*更多内容请看*[***plain English . io***](http://plainenglish.io)