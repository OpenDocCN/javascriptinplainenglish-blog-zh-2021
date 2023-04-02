# 如何使用 JavaScript 就地替换一个 DOM 元素？

> 原文：<https://javascript.plainenglish.io/how-to-replace-a-dom-element-in-place-using-javascript-e6aba3f8177f?source=collection_archive---------4----------------------->

![](img/3e77dce1feacf13d702c9544f52160e3.png)

Photo by [Grant Durr](https://unsplash.com/@blizzard88?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 JavaScript 替换 DOM 元素。

在本文中，我们将研究如何用 JavaScript 替换 DOM 元素。

# 使用 parentNode.replaceChild 方法

我们可以通过获取想要替换的元素的父元素，用 JavaScript 替换 DOM 元素。

然后我们可以在它上面调用`replaceChild`方法来替换元素，代替父元素的当前子元素。

例如，如果我们有下面的 HTML:

```
<div>
  hello world
</div>
```

然后我们可以通过写来进行替换:

```
const div = document.querySelector("div");
const span = document.createElement("span");
span.innerHTML = "hello james";
div.parentNode.replaceChild(span, div);
```

我们用`document.querySelector`得到 div。

然后我们创建一个 span，我们想用`document.createElement`替换 div。

接下来，我们通过设置`innerHTML`属性来设置 span 的内容。

最后，我们用`span`和`div`调用`div.parentNode.replaceChild`，用 span 替换 div。

现在我们应该看到“你好，詹姆斯”而不是“你好，世界”

# 使用 replaceWith 方法

用一个元素替换另一个元素的更简单的方法是使用`replaceWith`方法。

为了使用它，我们写:

```
const div = document.querySelector("div");
const span = document.createElement("span");
span.innerHTML = "hello james";
div.replaceWith(span);
```

在最后一行，我们用`span`调用`div.replaceWith`，用`span`替换`div`。

我们得到了和上一个例子一样的结果。

# 结论

我们可以通过获取想要替换的元素的父节点并在父节点上调用`replaceChild`来替换 DOM 元素。

或者我们可以调用我们想要替换的元素上的`replaceWith`并将我们想要替换的元素作为参数传入。

*更多内容看* [***说白了. io***](http://plainenglish.io/)