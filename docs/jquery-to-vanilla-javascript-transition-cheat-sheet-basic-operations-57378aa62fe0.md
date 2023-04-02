# jQuery 到普通 JavaScript 转换备忘单—基本操作

> 原文：<https://javascript.plainenglish.io/jquery-to-vanilla-javascript-transition-cheat-sheet-basic-operations-57378aa62fe0?source=collection_archive---------16----------------------->

![](img/5235c4580a6d4fadead5d747350b1e99.png)

Photo by [Timothy Eberly](https://unsplash.com/@timothyeberly?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

浏览器中的普通 JavaScript 现在内置了 jQuery 的许多特性，

因此，我们不需要使用 jQuery 做很多事情。

在本文中，我们将研究 jQuery 特性的普通 JavaScript 等价物。

# 选择元素

我们可以使用`querySelector`方法用普通 JavaScript 中给定的选择器选择单个元素。

Vanilla JavaScript 还有一个`querySelectorAll`方法，可以用给定的选择器选择多个元素。

例如，我们可以写:

```
document.querySelector("div");
```

选择文档中的第一个 div。

并选择所有 div:

```
document.querySelectorAll("div");
```

`querySelectorAll`返回一个 NodeList 对象，这是一个可迭代对象，其中包含所有选定的节点。

在 jQuery 中，我们有:

```
$("div");
```

选择所有的 div。

# 对所有选定的元素运行函数

在 jQuery 中，我们可以对所有选中的元素运行一个函数。

例如，我们可以通过编写以下内容来隐藏所有 div:

```
$("div").hide();
```

为了用普通的 JavaScript 做同样的事情，我们可以使用`forEach`方法:

```
document.querySelectorAll("div")
  .forEach(div => {
    div.style.display = "none"
  })
```

我们也可以使用 for-of 循环:

```
for (const div of document.querySelectorAll("div")) {
  div.style.display = "none"
}
```

`querySelector`返回的 NodeList 也可以传播:

```
const divs = [...document.querySelectorAll("div")]
divs
  .forEach(div => {
    div.style.display = "none"
  })
```

`divs`现在是数组而不是节点列表。

这意味着我们可以在上面运行许多数组方法。

# 在一个元素中寻找另一个元素

为了用 jQuery 在另一个元素中找到一个元素，我们使用了`find`方法:

```
const div = $("div");
//...
div.find(".box");
```

为了用普通的 JavaScript 做同样的事情，我们可以用`querySelector`来查找一个元素，用`querySelectorAll`用给定的选择器来查找该元素的所有实例。

所以我们写道:

```
const div = document.querySelector('div')
//...
div.querySelector(".box");
```

查找 div 中第一个包含类`box`的元素。

我们写道:

```
const div = document.querySelector('div')
//...
div.querySelectorAll(".box");
```

查找 div 中所有带有类`box`的元素。

# 用`parent()`、`next()`和`prev()`遍历树

jQuery 有`parent`方法来获取元素的父元素。

jQuery 的`next`方法返回一个元素的下一个兄弟元素。

而 jQuery 的`prev`方法返回一个元素的前一个兄弟元素。

要使用它们，我们可以写:

```
$("div").next();
$("div").prev();
$("div").parent();
```

在普通的 JavaScript 中，我们可以写:

```
const div = document.querySelector("div");
div.nextElementSibling;
div.previousElementSibling;
div.parentElement;
```

`nextElementSibling`返回下一个同级元素。

`previousElementSibling`返回上一个同级元素。

并且`parentElement`返回父元素。

# 处理事件

jQuery 让我们可以轻松地向元素添加事件处理程序。

例如，我们可以写:

```
$("button").click((e) => {
  /* handle click event */
});
$("button").mouseenter((e) => {
  /* handle click event */
});
$(document).keyup((e) => {
  /* handle key up event */
});
```

在选中的元素上分别添加一个`click` 事件处理程序、`mouseenter` 事件处理程序和`keyup` 事件处理程序。

为了用普通的 JavaScript 做同样的事情，我们可以使用`addEventListener`方法:

```
document
  .querySelector("button")
  .addEventListener("click", (e) => {
    /* ... */
  });document
  .querySelector("button")
  .addEventListener("mouseenter", (e) => {
    /* ... */
  });document
  .addEventListener("keyup", (e) => {
    /* ... */
  });
```

我们只需选择带有`querySelector`的元素，并调用`addEventListener`，将事件名称作为第一个参数，将事件处理程序回调作为第二个参数。

# 结论

我们可以用普通的 JavaScript 完成许多基本的 DOM 操作，比如选择元素、遍历 DOM 树以及向元素添加事件监听器。

*更多内容请看*[***plain English . io***](http://plainenglish.io)