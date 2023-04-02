# 如何在当前光标位置的文本区域插入文本？

> 原文：<https://javascript.plainenglish.io/how-to-insert-text-into-the-text-area-at-the-current-cursor-position-23a0baf0ddd9?source=collection_archive---------4----------------------->

![](img/012be36d9992480eb39ac8e648ec7784.png)

Photo by [Lucian Dachman](https://unsplash.com/@luciandachman?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在当前光标位置的文本区域插入文本。

在本文中，我们将研究如何在当前光标位置向文本区域插入文本。

# 使用 setRangeText 方法

我们可以使用`setRangeText`方法在当前光标位置添加文本。

例如，如果我们有以下输入:

```
<input id="input"/>
```

然后，我们可以编写以下 JavaScript 代码，在光标位于输入中并按下 Enter 键时，在光标位置添加文本:

```
const typeInTextarea = (newText, el = document.activeElement) => {
  const [start, end] = [el.selectionStart, el.selectionEnd];
  el.setRangeText(newText, start, end, 'select');
}document.getElementById("input").onkeydown = e => {
  if (e.key === "Enter") {
    typeInTextarea("abc");
  }
}
```

我们创建了一个`typeInTextarea`函数，它的`newText`参数包含了我们想要插入的文本。

并且它有`el`元素，该元素有我们想要插入文本的元素。

`document.activeElement`是当前关注的元素。

在函数中，我们用`selectionStart`和`selectionEnd`得到选择开始和选择结束。

然后我们用`newText`、`start`、`end`和`'selection'`调用`setRangeText`，在当前光标位置添加`newText`。

然后我们将`onkeydown`属性设置为一个函数，该函数调用`typeInTextarea`函数，并按下 enter 键来插入我们想要插入的文本。

# 结论

当我们用`setRangeText`方法按下一个键时，我们可以将文本插入光标位置的输入中。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)