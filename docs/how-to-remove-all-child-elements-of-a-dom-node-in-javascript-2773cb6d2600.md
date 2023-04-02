# 如何在 JavaScript 中移除一个 DOM 节点的所有子元素？

> 原文：<https://javascript.plainenglish.io/how-to-remove-all-child-elements-of-a-dom-node-in-javascript-2773cb6d2600?source=collection_archive---------10----------------------->

![](img/0a10bea4bec3ce3ecbdc3be35261b65e.png)

Photo by [Caleb Woods](https://unsplash.com/@caleb_woods?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从 DOM 节点中移除所有子元素是我们有时在 JavaScript 中不得不做的事情。

在本文中，我们将研究如何用 JavaScript 移除 DOM 节点的所有子元素。

# 清除 innerHTML

移除元素的所有子元素的一种方法是将元素的`innerHTML`属性设置为空字符串。

例如，如果我们有以下 HTML:

```
<button>
  clear
</button>
<div>
</div>
```

然后，我们可以编写以下 JavaScript 来将元素添加到 div 中。

当我们单击“清除”按钮时，可以清除这些项目:

```
const div = document.querySelector('div')
const button = document.querySelector('button')for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  div.appendChild(p)
}button.addEventListener('click', () => {
  div.innerHTML = ''
})
```

我们用`document.querySelector`得到 div 和按钮。

然后在 for 循环中，我们创建了`p`元素并将它们添加到 div 中。

然后我们调用`button`上的`addEventListener`，用`'click'`作为第一个参数来添加一个点击监听器。

然后在回调中，我们将`div.innerHTML`设置为空字符串，以便在单击按钮时清除其内容。

# 清除`textContent`

我们可以不清除`innerHTML`，而是清除`textContent`。

为此，我们写道:

```
const div = document.querySelector('div')
const button = document.querySelector('button')for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  div.appendChild(p)
}button.addEventListener('click', () => {
  div.textContent = ''
})
```

我们只是把`innerHTML`换成`textContent`。

其余的代码都是一样的。

# 循环移除每个`lastChild from the DOM`

我们可以用`removeChild`方法从 DOM 中移除一个元素的所有子元素。

例如，我们可以写:

```
const div = document.querySelector('div')
const button = document.querySelector('button')for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  div.appendChild(p)
}button.addEventListener('click', () => {
  while (div.firstChild) {
    div.removeChild(div.lastChild);
  }
})
```

我们在点击监听器中有一个`while`循环。

我们检查带有`div.firstChild`的`div`中是否有任何`firstChild`元素。

如果有，我们调用`removeChuld`删除`div.lastChild`，直到没有`firstChild`存在。

# 循环删除每一个`lastElementChild from the DOM`

我们也可以从一个元素中删除所有的`lastElementChild`。

为此，我们写道:

```
const div = document.querySelector('div')
const button = document.querySelector('button')for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = 'hello'
  div.appendChild(p)
}button.addEventListener('click', () => {
  while (div.lastElementChild) {
    div.removeChild(div.lastElementChild);
  }
})
```

`lastElementChild`返回给定元素的最后一个子元素。

我们可以调用`removeChild`来删除它们，直到什么也不剩。

# 结论

我们可以通过设置`innerHTML`或`textContent`很容易地移除一个元素的所有子元素。

同样，我们可以用`removeChild`逐个移除子元素。

*更多内容看*[***plain English . io***](http://plainenglish.io)