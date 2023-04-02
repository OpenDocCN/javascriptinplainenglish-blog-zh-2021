# jQuery 到普通 JavaScript 转换备忘单—等待文档加载、类和 HTTP 请求

> 原文：<https://javascript.plainenglish.io/jquery-to-vanilla-javascript-transition-cheat-sheet-wait-for-document-load-classes-and-http-b4395175eaf8?source=collection_archive---------25----------------------->

![](img/8a58f0e9ce237efedc89fcbff97b1542.png)

Photo by [Geert Pieters](https://unsplash.com/@shotsbywolf?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

浏览器中的普通 JavaScript 现在内置了 jQuery 的许多特性。

因此，我们不需要使用 jQuery 做很多事情。

在本文中，我们将研究 jQuery 特性的普通 JavaScript 等价物。

# 等待文档准备就绪

使用 jQuery，我们可以在加载 DOM 时使用`$(document).ready`回调来运行代码:

```
$(document).ready(() => {
  //...
});
```

为了用普通的 JavaScript 做同样的事情，我们可以在`document`上监听`DOMContentLoaded`事件:

```
document.addEventListener("DOMContentLoaded", () => {
  //...
});
```

# 使用类

jQuery 有一些方法可以让我们添加、删除或切换元素的类:

```
$("div").addClass("focus");
$("div").removeClass("focus");
$("div").toggleClass("focus");
```

`addClass`让我们将`focus`类添加到 div 中。

`removeClass`让我们将`focus`类移至 div。

`toggleClass`让我们将`focus`类切换到 div。

为了用普通的 JavaScript 做同样的事情，我们可以使用元素的`classList`属性中的方法。

例如，我们可以写:

```
const div = document.querySelector("div");
div.classList.add("focus");
div.classList.remove("focus");
div.classList.toggle("focus");
```

`classList.add`增加了`focus`类。

`classList.remove`删除`focus`类。

并且`classList.toggle`切换`focus`类。

我们还可以通过以下方式添加或删除多个类:

```
const div = document.querySelector("div");
div.classList.add("focus", "highlighted");
div.classList.remove("focus", "highlighted");
```

`classList.add`增加了`focus`和`highlighted`类。

`classList.remove`删除`focus`和`highlighted`类。

我们也可以使用`classList.replace`方法用另一个类替换一个类。

例如，我们可以写:

```
document.querySelector("div").classList.replace("focus", "blurred");
```

将`focus`级替换为带有`classList.replace`的`blurred`级。

# 检查元素是否有类

jQuery 附带了`hasClass`方法来检查一个元素是否有给定的类。

例如，我们可以写:

```
if ($("div").hasClass("focus")) {
  //...
}
```

为了用普通的 JavaScript 做同样的事情，我们可以使用`classList.contains`方法:

```
if (document.querySelector("div").classList.contains("focus")) {
  //...
}
```

# 网络请求

jQuery 附带了`get`方法来发出 GET 请求。

它还附带了`ajax`方法，让我们可以提出任何请求。

例如，我们可以通过编写来使用`ajax`:

```
$.ajax({
  url: "https://yesno.wtf/api"
}).done((data) => {
  console.log(data)
}).fail(() => {
  // Handle error
});
```

我们可以通过写来使用`get`:

```
$.get({
  url: "https://yesno.wtf/api"
}).done((data) => {
  console.log(data)
}).fail(() => {
  // Handle error
});
```

对于普通的 JavaScript，我们可以只使用`fetch`方法:

```
(async () => {
  try {
    const res = await fetch('https://yesno.wtf/api')
    const data = await res.json()
    console.log(data)
  } catch (error) {
    console.log(error)
  }
})()
```

我们调用`res.json`将 JSON 响应数据对象转换成 JavaScript 对象。

`fetch`返回一个比使用`done`和`fail`回调更方便的承诺。

# 结论

我们可以使用普通的 JavaScript 来等待 DOM 准备好，发出 HTTP 请求，并轻松地操作元素类。

*更多内容请看*[***plain English . io***](http://plainenglish.io)