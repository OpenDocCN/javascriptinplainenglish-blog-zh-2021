# 如何像用鼠标突出显示一样以编程方式选择元素中的文本？

> 原文：<https://javascript.plainenglish.io/how-to-select-text-in-an-element-programmatically-like-highlighting-with-a-mouse-e8a6c03491cf?source=collection_archive---------4----------------------->

![](img/4e6fd5f18f0cd88687ec4bc3ad8ded0c.png)

Photo by [Ricky Kharawala](https://unsplash.com/@sweetmangostudios?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在网页上以编程方式选择元素中的文本。

在本文中，我们将研究如何像用户用鼠标突出显示文本一样以编程方式选择元素中的文本。

# window.getSelection 方法

我们可以使用`window.getSelection`方法来选择元素中的文本。

例如，如果我们有下面的 HTML:

```
<div>
  foo
</div>
```

然后我们通过书写来调用`window.getSelection`:

```
const node = document.querySelector('div');
if (window.getSelection) {
  const selection = window.getSelection();
  const range = document.createRange();
  range.selectNodeContents(node);
  selection.removeAllRanges();
  selection.addRange(range);
}
```

我们调用`window.getSelection`来创建`seldction`对象。

然后我们调用`document.createRange`来创建选择范围。

然后我们用`node`对象调用`range.selectNodeContents`来选择给定元素的内容。

接下来，我们调用`selectionRemoveAllRanges`来删除所有先前选择的内容。

最后，我们用`range`调用`selection.addRange`来选择当前选中的文本。

非 Internet Explorer 浏览器可用的`window.getSelection`方法。

# 结论

我们可以使用`window.getSelection`方法来选择元素中的文本。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)