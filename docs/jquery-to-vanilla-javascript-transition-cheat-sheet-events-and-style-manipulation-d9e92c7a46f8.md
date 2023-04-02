# jQuery 到普通 JavaScript 的过渡备忘单—事件和样式操作

> 原文：<https://javascript.plainenglish.io/jquery-to-vanilla-javascript-transition-cheat-sheet-events-and-style-manipulation-d9e92c7a46f8?source=collection_archive---------15----------------------->

![](img/70c5f36b2bd1a01d72da877e84d416d8.png)

Photo by [CHUTTERSNAP](https://unsplash.com/@chuttersnap?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

浏览器中的普通 JavaScript 现在内置了 jQuery 的许多特性。

因此，我们不需要使用 jQuery 做很多事情。

在本文中，我们将研究 jQuery 特性的普通 JavaScript 等价物。

# 事件监听动态添加的元素

在许多情况下，我们希望监听动态添加元素上的事件。

在 jQuery 中，我们将使用`on`方法来监听所有 select 元素上的事件。

例如，我们可以写:

```
$("div").on("click", ".search-result", (e) => {
  //...
});
```

为了监听点击 div 中带有`search-result`类的元素，使用`on`方法将事件监听器附加到它们上面。

为了用普通的 JavaScript 做同样的事情，我们可以使用事件委托。

例如，我们可以写:

```
document
  .querySelector('div')
  .addEventListener('click', (e) => {
    if (e.target.className === 'search-result') {
      //...
    }
  })
```

在 div 上调用`addEventListener`。

然后在点击事件处理程序中，我们使用`e.target.className`来获取我们点击的元素的类名。

然后我们进行比较，看看我们是否点击了带有类`search-result`的任何东西。

# 触发和创建事件

在 jQuery 中，我们可以使用`trigger`方法来触发事件。

例如，我们可以写:

```
$(document).trigger("myEvent");
$("div").trigger("myEvent");
```

为了用普通的 JavaScript 做同样的事情，我们编写:

```
document.dispatchEvent(new Event("myEvent"));
document.querySelector("div").dispatchEvent(new Event("myEvent"));
```

Wd 调用所选元素上的`dispatchEvent`来触发我们的 one 事件。

# 造型元素

jQuery 有`css`方法让我们设计元素的样式。

例如，我们可以写:

```
$("div").css("color", "#000");
```

为了用普通的 JavaScript 做同样的事情，我们可以写:

```
document.querySelector("div")
  .style.color = "#000";
```

我们设置`style.color`属性来设置所选 div 的 CSS `color`属性。

我们还可以将一个对象传入 jQuery 的`css`方法:

```
$("div").css({
  "color": "#000",
  "background-color": "red"
});
```

为了用普通 JavaScript 做同样的事情，我们只需将`style`对象属性设置为我们想要的值:

```
const div = document.querySelector("div");
div.style.color = "#000";
div.style.backgroundColor = "red";
```

我们也可以设置`style.cssText`属性来设置多种样式:

```
const div = document.querySelector("div");
div.style.cssText = "color: #000; background-color: red";
```

# `hide()`和`show()`

jQuery 附带了`hide`方法，让我们隐藏选中的元素。

我们可以使用 jQuery 的`show`方法来显示选中的元素。

例如，我们可以写:

```
$("div").hide();
$("div").show();
```

分别隐藏和显示 div。

为了对普通 JavaScript 做同样的事情，我们可以将`display` CSS 属性设置为我们想要的 JavaScript 值:

```
document.querySelector("div").style.display = "none";
document.querySelector("div").style.display = "block";
```

我们通过将`style.display`设置为`'none'`来隐藏 div。

我们通过将`style.display`设置为`'block'`来显示 div。

# 结论

我们可以使用普通浏览器 JavaScript 轻松添加事件监听器和操纵样式。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)