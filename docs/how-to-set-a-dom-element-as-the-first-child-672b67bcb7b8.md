# 如何将 DOM 元素设置为第一个子元素

> 原文：<https://javascript.plainenglish.io/how-to-set-a-dom-element-as-the-first-child-672b67bcb7b8?source=collection_archive---------12----------------------->

![](img/195b46031db824b975f66ef3b547c922.png)

Photo by [Tanaphong Toochinda](https://unsplash.com/@daen_2chinda?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望将一个 DOM 元素设置为第一个子元素。

在本文中，我们将研究将 DOM 元素设置为第一个子元素的方法。

# 使用 prepend 方法

在现代浏览器中，HTML 元素对象带有`prepend`方法，让我们将一个元素作为第一个子元素。

例如，如果我们有下面的 HTML:

```
<div>
  <p>
    bar
  </p>
  <p>
    baz
  </p>
</div>
```

然后，我们可以编写以下 JavaScript，将一个元素作为 div 的第一个子元素添加到前面:

```
const div = document.querySelector('div')
const newChild = document.createElement('p')
newChild.textContent = 'foo'
div.prepend(newChild)
```

我们用`document.querySelector`方法得到 div。

然后我们调用`document.createElement`来创建一个元素。

接下来，我们设置`textContent`属性，向我们创建的 p 元素添加一些内容。

然后我们调用`div.prepend`将`newChild`作为 div 的第一个子元素。

还有一个`append`方法将一个元素作为父元素的最后一个子元素追加。

# 使用 insertAdjacentElement 方法

我们还可以使用`insertAdjacentElement`方法来插入一个元素，作为该元素的第一个子元素。

例如，如果我们有相同的 HTML:

```
<div>
  <p>
    bar
  </p>
  <p>
    baz
  </p>
</div>
```

然后我们可以写:

```
const div = document.querySelector('div')
const newChild = document.createElement('p')
newChild.textContent = 'foo'
div.insertAdjacentElement('afterbegin', newChild)
```

用`'afterbegin'`和`newChild`调用`insertAdjacentElement`，将`newChild`作为 div 的第一个子元素。

`insertAdjacentElement`第一个参数的其他可能值为:

*   `beforebegin`:元素本身之前。
*   `beforeend`:就在元素内部，在它的最后一个子元素之后。
*   `afterend`:元素本身之后。

# 使用 insertBefore 方法

我们可以用来将一个元素作为第一个子元素的另一种方法是使用`insertBefore`方法。

例如，我们可以写:

```
const div = document.querySelector('div')
const newChild = document.createElement('p')
newChild.textContent = 'foo'
if (div.firstChild) {
  div.insertBefore(newChild, div.firstChild);
} else {
  div.appendChild(childNode);
}
```

假设我们在前面的例子中有相同的 HTML，将`newChild`作为 div 的第一个子元素。

我们检查是否有一个`firstChild`元素附加到 div 上。

如果有，那么我们调用`insertBefore`在 div 的`firstChild`前插入`newChild`。

否则我们只是调用`appendChild`追加`newChild`作为子元素。

# 结论

我们可以使用各种 HTML 元素方法将一个元素作为父元素的第一个子元素。

*更多内容看*[***plain English . io***](http://plainenglish.io)