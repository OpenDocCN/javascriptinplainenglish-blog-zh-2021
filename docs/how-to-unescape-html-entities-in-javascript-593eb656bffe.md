# 如何在 JavaScript 中取消 HTML 实体的转义？

> 原文：<https://javascript.plainenglish.io/how-to-unescape-html-entities-in-javascript-593eb656bffe?source=collection_archive---------9----------------------->

![](img/e7a66ea02c2a05e02d721604a6758165.png)

Photo by [Marek Szturc](https://unsplash.com/@marxgall?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在 web 应用程序中取消字符串与 HTML 实体的转义。

在本文中，我们将研究如何在 JavaScript 中取消 HTML 实体的转义。

# 使用文本区域取消隐藏 HTML 实体

取消 HTML 实体转义的一种方法是将转义文本放在文本区域中。

这将取消文本的转义，因此我们可以通过从文本区域获取文本来返回未转义的文本。

例如，我们可以写:

```
const htmlDecode = (input) => {
  const e = document.createElement('textarea');
  e.innerHTML = input;
  return e.childNodes.length === 0 ? "" : e.childNodes[0].nodeValue;
}const result = htmlDecode("&lt;img src='myimage.jpg'&gt;");
console.log(result)
```

我们有一个`htmlDecode`函数，它将一个`input`字符串作为参数。

在函数中，我们用`document.createElement`创建了`textarea`元素。

然后我们将它的`innerHTML`设置为`input`。

然后我们通过获取`childNodes[0].nodeValue`属性得到未转义的文本并返回它。

现在，当我们传入一个转义字符串时，我们将得到未转义的版本。

于是`“&lt;img src=’myimage.jpg’&gt;”`变成了`"<img src=’myimage.jpg’>"`。

# 使用 DOM parser . prototype . parsefromstring 方法

另一种取消字符串转义的方法是使用`DOMParser.prototype.parseFromString`方法。

为了使用它，我们传入转义的字符串，以及要返回的字符串的 MIME 类型。

例如，我们可以这样使用它:

```
const htmlDecode = (input) => {
  const doc = new DOMParser().parseFromString(input, "text/html");
  return doc.documentElement.textContent;
}const result = htmlDecode("&lt;img src='myimage.jpg'&gt;");
console.log(result)
```

我们创建一个新的`DOMParser`实例。

然后我们用`input`字符串和要转换到的字符串的 MIME 类型字符串调用`parseFromString`。

然后用`doc.documentElement.textContent`获取未转义的字符串并返回。

因此，`result`将与前面的示例相同。

# 用 Div 取消对 HTML 实体的屏蔽

我们还可以创建一个 div，将其`innerHTML`属性设置为转义字符串。

然后我们可以从`innerText`属性中获得未转义的字符串。

为此，我们写道:

```
const htmlDecode = (input) => {
  const e = document.createElement('div');
  e.innerHTML = input;
  return e.innerText
}const result = htmlDecode("&lt;img src='myimage.jpg'&gt;");
console.log(result)
```

我们将`e.innerHTML`设置为`input`。

然后我们返回`e.innerText`来返回未转义的文本。

所以我们得到了和前面例子一样的结果。

# 结论

在 JavaScript 中，我们可以使用几种方法来取消字符串与 HTML 实体的转义。

*更多内容请看*[***plain English . io***](http://plainenglish.io)