# 如何用 JavaScript 遍历一个页面上的所有 DOM 元素？

> 原文：<https://javascript.plainenglish.io/how-to-loop-through-all-dom-elements-on-a-page-with-javascript-c02741ebf767?source=collection_archive---------4----------------------->

![](img/9a72c6fdbe29878327acefdf0c2be386.png)

Photo by [amir rabiee](https://unsplash.com/@amir__rbe?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时我们想用 JavaScript 遍历页面上的所有 DOM 元素。

在本文中，我们将看看如何用 JavaScript 遍历页面上的所有 DOM 元素。

# 使用 document.getElementsByTagName 选择所有元素

我们可以用`document.getElementsByTagName`方法选择页面上的所有元素。

例如，如果我们有下面的 HTML:

```
<div>
  <span>hello world</span>
</div>
<p>
  how are you
</p>
```

然后，我们可以通过编写以下代码来遍历所有这些文件:

```
const allEls = document.getElementsByTagName("*");
for (const el of allEls) {
  console.log(el)
}
```

我们通过用`'*'`调用`document.getElementsByTagName`来选择所有元素。

然后我们可以用 for-of 循环遍历所有返回的元素。

# 使用 document . query select All 选择所有元素

我们可以用`document.querySelectorAll` 方法选择页面上的所有元素。

例如，如果我们有下面的 HTML:

```
<div>
  <span>hello world</span>
</div>
<p>
  how are you
</p>
```

然后，我们可以通过编写以下代码来遍历所有这些文件:

```
const allEls = document.querySelectorAll("*");
for (const el of allEls) {
  console.log(el)
}
```

我们通过用`'*'`调用`document.querySelectorAll` 来选择所有元素。

然后我们可以用 for-of 循环遍历所有返回的元素。

# 结论

我们可以使用`document.getElementsByTagName`或`document.querySelectorAll`方法来获取页面上的所有元素。

然后我们可以用 for-of 循环遍历它们。

*更多内容请看*[***plain English . io***](http://plainenglish.io)