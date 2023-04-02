# 如何用 JavaScript 监听带有 contenteditable 属性的 HTML 元素的变化？

> 原文：<https://javascript.plainenglish.io/how-to-listen-for-changes-to-html-elements-with-the-contenteditable-attribute-with-javascript-b715eeb4431e?source=collection_archive---------3----------------------->

![](img/19493f474f4374b33c6f49de04c58d4b.png)

Photo by [Arnel Hasanovic](https://unsplash.com/@arnelhasanovic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

添加了`contenteditable`属性的元素允许用户编辑元素内部的内容。

有时，我们可能希望监听对元素进行的更改事件。

在本文中，我们将看看如何监听应用了`contenteditable`属性的元素中触发的更改。

# 侦听元素发出的输入事件

当我们改变添加了`contenteditable`属性的元素的内容时，就会发出`input`事件。

因此，我们可以监听元素的`input`事件来监听其内容的变化。

例如，我们可以编写以下 HTML:

```
<div contenteditable>
  hello world
</div>
```

然后我们可以用`addEventListener`添加一个事件监听器:

```
const div = document.querySelector("div")
div.addEventListener("input", (e) => {
  console.log(e);
}, false);
```

当我们更改 div 中的内容时，我们将看到`input`事件监听器运行。

我们可以用`e.target`属性获得元素的属性和样式。

`e.timestamp`属性是创建事件的时间，以毫秒为单位。

# `MutationObserver`

我们还可以使用`MutationObserver`来观察元素内容的变化。

这是因为它可以监听 DOM 中的变化，包括元素中的任何内容变化。

例如，我们可以写:

```
const div = document.querySelector("div")
const observer = new MutationObserver((mutationRecords) => {
  console.log(mutationRecords[0].target.data)
})
observer.observe(div, {
  characterData: true,
  subtree: true,
})
```

并保持 HTML 不变。

我们传递一个带有`mutationRecords`对象的回调来获取突变记录。

`chartacterData`设置为`true`表示我们观察文本内容的变化。

将`subtree`设置为`true`意味着我们观察元素的 DOM 子树变化。

我们用`mutationRecords[0].target.data`属性获取 div 的最新内容。

# 结论

我们可以通过应用了`MutationObserver`的`contenteditable`属性来观察 HTML 内容的变化，或者监听元素的`input`事件。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*