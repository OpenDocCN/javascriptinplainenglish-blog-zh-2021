# 如何用 JavaScript 监听动态创建的元素上的事件？

> 原文：<https://javascript.plainenglish.io/how-to-listen-to-events-on-dynamically-created-elements-with-javascript-1d300d17d0e?source=collection_archive---------8----------------------->

![](img/1771e29713327feb3aa90f43d3a2b4c9.png)

Photo by [Arnold Antoo](https://unsplash.com/@arnold_antoo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

网页中的许多项目都是用 JavaScript 动态创建的。

这意味着我们必须监听它们发出的事件，这样我们就可以使用它们做一些事情，而不是静态地显示内容。

在本文中，我们将了解如何监听用 JavaScript 动态创建的元素上的事件。

# 事件委托

我们可以监听在具有动态创建的元素的容器元素上发出的事件。

在事件监听器中，我们可以检查哪个项目正在发出事件，根据发出事件的元素来做我们想要的事情。

这是可能的，因为一个元素发出的事件会向上冒泡到它的父元素和祖先元素，一直到`body`和`html`元素，除非我们手动停止它。

因此，如果我们允许事件传播，`body`元素的事件监听器将从它的所有后代元素中选取事件。

例如，我们可以编写以下 HTML:

```
<div></div>
```

然后编写以下 JavaScript 来监听由动态创建的`p`元素发出的点击事件:

```
const div = document.querySelector('div')
for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.className = i % 2 === 1 ? 'odd' : 'even'
  p.textContent = 'hello'
  div.appendChild(p)
}document.addEventListener('click', (e) => {
  if (e.target.className.includes('odd')) {
    console.log('odd element clicked', e.target.textContent)
  } else if (e.target.className.includes('even')) {
    console.log('even element clicked', e.target.textContent)
  }
});
```

在上面的代码中，我们用`document.querySelector`获得了 div 元素。

然后我们使用 for 循环在 div 内部添加`p`元素 100 次。

我们设置元素的`className`来设置`class`属性的值。

`textContent`有`p`元素的内容值。

然后我们调用 div 上的`appendChild`来添加 div 中的`p`元素。

然后为了监听我们刚刚添加的`p`元素上的点击事件，我们监听`document`的点击，它是`body`元素。

我们调用`addEventListener`将点击监听器添加到`body`元素中。

然后我们传入一个回调函数作为`addEventListener`的第二个参数。

`e`参数是事件对象。

它包含关于发出事件的原始元素的信息。

我们用`e.target`属性获取最初发出事件的元素。

因此，我们可以获得具有`e.target.className`属性的元素的`class`属性的值。

我们用属性`e.target.textContent`得到属性`textContent`的值。

# 结论

我们可以通过事件委托来监听由动态创建的 HTML 元素发出的事件。

我们只是监听来自发出事件的元素的祖先的事件，然后检查哪个元素在回调中发出了事件。

*更多内容看*[***plain English . io***](http://plainenglish.io/)