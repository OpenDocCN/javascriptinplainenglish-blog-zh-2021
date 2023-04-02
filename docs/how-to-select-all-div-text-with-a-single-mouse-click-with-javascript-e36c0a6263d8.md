# 如何用 JavaScript 鼠标一点就选中所有 Div 文本？

> 原文：<https://javascript.plainenglish.io/how-to-select-all-div-text-with-a-single-mouse-click-with-javascript-e36c0a6263d8?source=collection_archive---------10----------------------->

![](img/d3e7b975ba5f5a6ce75b14d86b420960.png)

Photo by [Ryan Stone](https://unsplash.com/@rstone_design?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望用 JavaScript 通过单击鼠标来选择所有 div 文本。

在本文中，我们将研究如何用 JavaScript 通过单击鼠标来选择所有的 div 文本。

# 使用 document.body.createTextRange 或 document.createRange 方法

我们可以使用`document.body.createTextRange`或`document.createRange`方法来创建一个选择。

例如，如果我们有下面的 HTML:

```
<div id="selectable">http://example.com/page.htm</div>
```

然后我们可以编写下面的代码:

```
const selectable = document.getElementById('selectable')
selectable.addEventListener('click', () => {
  if (document.selection) { 
    const range = document.body.createTextRange();
    range.moveToElementText(selectable);
    range.select();
  } else if (window.getSelection) {
    const range = document.createRange();
    range.selectNode(selectable);
    window.getSelection().removeAllRanges();
    window.getSelection().addRange(range);
  }
})
```

向 div 添加一个单击侦听器，并在我们单击它时选择 div 中的文本。

为此，我们调用`getElementById`来选择 div。

然后我们用`'click'`调用`addEventListener`来为它添加一个点击监听器。

在回调中，如果定义了`document.selection`，我们调用`documebnt.create.createTextRange`方法来创建一个选择。

如果代码在 IE 中运行，则定义这一点。

然后我们调用`moveToElementText`将光标移动到文本内容。

然后我们调用`select`来高亮显示所有的文本。

在所有其他浏览器上，我们调用`document.createRange`来创建选择。

然后我们调用`selectNode`,使用包含我们想要创建选择的内容的元素。

然后我们调用`removeAllRanges`来删除所有已经存在的选中的条目。

最后，我们用`range`调用`addRange`来选择我们创建的选择范围。

现在，当我们单击 div 文本时，该文本将被选中。

# 结论

当我们点击 div 文本时，我们可以通过创建一个选择对象来选择所有的文本，然后选择文本。

*更多内容看* [***说白了. io***](http://plainenglish.io/)