# 如何用 JavaScript 观察 DOM 的变化？

> 原文：<https://javascript.plainenglish.io/how-to-watch-for-dom-changes-with-javascript-311c5deeb270?source=collection_archive---------1----------------------->

![](img/3942eda47d8a3e0555cbb34a3ae71366.png)

Photo by [Marita Kavelashvili](https://unsplash.com/@maritafox?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望观察 web 应用程序中 DOM 的变化。

在本文中，我们将看看如何用 JavaScript 观察 DOM 中的变化。

# `MutationObserver`

在我们的 JavaScript web 应用程序中观察 DOM 变化的一种方法是使用`MutationObserver`构造函数。

例如，我们可以写:

```
const observer = new MutationObserver((mutations, observer) => {
  console.log(mutations, observer);
});observer.observe(document, {
  subtree: true,
  attributes: true
});const sleep = ms => new Promise(resolve => setTimeout(resolve, ms));(async () => {
  for (let i = 0; i < 5; i++) {
    const p = document.createElement('p')
    p.textContent = 'hello'
    document.body.appendChild(p)
    await sleep(1000)
  }
})();
```

用一个循环创建`MutationObserver`实例，将子元素添加到异步函数的主体中。

我们在 1 秒钟后插入一个新的 p 元素 5 次。

我们将回调传递给在 DOM 改变时运行的`MutationObserver`构造函数。

然后，我们在想要观察变化的元素上调用`observe`。

`subtree`设置为`true`意味着我们观察子元素的变化。

`attributes`设置为`true`意味着我们观察元素属性的变化。

其他选项包括:

*   `childList` —设置为`true`观察目标的孩子
*   `characterData` —设置为`true`观察目标的数据
*   `attributeOldValue` —设置为`true`以观察 DOM 更改前元素的属性值
*   `characterDataOldValue` —设置为`true`，在改变前观察目标的角色数据
*   `attributeFilter` —设置为要观察的属性的本地名称。

`mutations`参数有一组应用了更改的属性。

`mutations.target`属性的目标元素已经改变。

`mutations.target.lastChild`在被监视的元素中有最底层的子节点。

`mutations.target.lastElementChild`在被监视的元素中有最底层的子元素节点。

# 侦听 DOMSubtreeModified 事件

另一种监听 DOM 结构变化的方法是监听`DOMSubtreeModified`事件。

例如，我们可以写:

```
document.addEventListener('DOMSubtreeModified', (e) => {
  console.log(e)
})const sleep = ms => new Promise(resolve => setTimeout(resolve, ms));(async () => {
  for (let i = 0; i < 5; i++) {
    const p = document.createElement('p')
    p.textContent = 'hello'
    document.body.appendChild(p)
    await sleep(1000)
  }
})();
```

为文档的`DOMSubtreeModified`事件添加一个事件监听器。

`e`参数是一个`MutationEvent`对象。

属性的元素已经改变。

`e.path`具有指向已更改元素的路径，作为指向已更改元素的元素数组。

`e.children`具有一个元素已更改的 HTMLCollection 对象。

# 结论

我们可以使用`MutationObserver`和`DOMSubtreeModified`事件来监听 DOM 的变化。