# 如何限制 HTML 文本输入只允许数字？

> 原文：<https://javascript.plainenglish.io/how-to-restrict-html-text-input-to-only-allow-numbers-6b96ca3869f6?source=collection_archive---------7----------------------->

![](img/8acf4df9dc5dfce7bce021a9fd86be3e.png)

Photo by [Erik Mclean](https://unsplash.com/@introspectivedsgn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们只想让用户在 HTML 文本输入中输入数字。

在这篇文章中，我们将看看如何限制 HTML 文本输入只允许数字。

# 观看按键

我们可以通过检查输入的值和粘贴的数据来观察按键。

为此，我们编写以下 HTML:

```
<input type="text" />
```

我们可以编写下面的 JavaScript:

```
const input = document.querySelector("input");
input.addEventListener("keypress", (evt) => {
  const theEvent = evt || window.event;
  let key = theEvent.keyCode || theEvent.which;
  key = String.fromCharCode(key);
  const regex = /[0-9]|\./;
  if (!regex.test(key)) {
    theEvent.returnValue = false;
    if (theEvent.preventDefault) theEvent.preventDefault();
  }
});
```

我们用事件监听器监听`keypress`事件。

在`keypress`事件回调中，我们通过获取`keyCode`属性来获取代码。

然后我们得到按下`String.fromCharCode`键的值。

然后我们调用`regex.test`来检查键值是否是一个数字。

如果不是，那么我们调用`preventDefault()`来防止字符被添加到输入的值字符串中。

此外，我们可以从输入的值字符串中删除所有非数字字符。

例如，我们可以写:

```
const input = document.querySelector("input");
input.addEventListener("keyup", (evt) => {
  input.value = evt.target.value.replace(/[^\d]/, "");
});
```

我们用`evt.target.value`得到输入的值。

我们调用`replace`来获取所有非数字字符和一个空字符串。

然后我们将返回的字符串赋给`input.value`来更新输入的值。

# 将输入类型属性设置为数字

同样，我们可以将输入的`type`属性设置为`number`。

为此，我们写道:

```
<input type='number' />
```

然后，我们不需要添加任何 JavaScript 代码来从输入的值字符串中删除非数字字符。

# 结论

有几种方法可以将输入值限制为数字。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)