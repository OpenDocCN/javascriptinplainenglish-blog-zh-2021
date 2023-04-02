# 如何选择、遍历和操作 DOM:初学者指南

> 原文：<https://javascript.plainenglish.io/selecting-traversing-and-manipulating-in-the-dom-3ea57ef5f4f4?source=collection_archive---------14----------------------->

![](img/c4eed527a35304b867ca3c14fcac8d92.png)

Photo by [Florian Olivo](https://unsplash.com/@florianolv?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您计划成为一名前端开发人员并构建视觉上吸引人的用户界面(UI)，您需要成为 DOM 的好朋友。遍历 DOM 是每个 web 开发人员必须掌握的基本技能。我知道这个话题对初学程序员来说是多么令人生畏，所以我安排了一些基本技巧来帮助您开始 DOM 之旅。

## 什么是 DOM？

DOM 是文档对象模型的首字母缩写。它基本上是你的 HTML 文件的副本，被构造成一个“树”,其中每个元素(在根中)都是一个对象，这意味着我们可以对它们调用 JavaScript 方法。这允许我们在不改变原始 HTML 文件的情况下对网页进行修改，例如添加文本或删除图像。很酷，对吧？

## 选择 DOM 元素

第一步是选择要操作的元素。根据您想要选择的元素，有 5 种方法可以做到这一点。

*   getElementsByTagName()
*   getElementsByClassName()
*   getElementById()
*   查询选择器()
*   querySelectorAll()

就个人而言，我喜欢使用`querySelector()`和`querySelectorAll()`，因为您可以通过标签名、类名和 id 选择元素，还可以获得链接选择器的额外好处。例如，如果我们想在这个代码片段中选择< a >标签，我们可以写`document.querySelector(‘div a.in-div’)`，它读起来有点像英语，但是是倒过来的，类似于“选择一个`<a>`标签，在`<div>`标签内有一个`in-div`的 class ( `.`代表 class，`#`代表 id)。

```
<div>
    <p class='in-div'>Hello</p>
    <a class='in-div' src='www.greeting.com'>World</a>
<div/>
```

如果节点嵌套很深，这很快就会变得混乱。在这种情况下，只需向您试图选择的元素添加一个 id 或 class 属性，以便更容易获取该节点。

## 穿越大教堂

一旦我们选择了元素，我们可能希望从那里移动并选择附近的其他元素。有大量的方法和属性可以用来在节点之间移动。然而，这些是我发现自己经常使用的:

*   **childNodes** 返回一个 NodeList 对象，它类似于一个数组，包含嵌套在调用的元素中的所有元素。我们可以像处理数组一样循环遍历一个节点列表。
*   **next sibling&previous sibling**返回下面的元素(下一个)或上面的元素(上一个)。
*   **parentElement** 返回父元素。换句话说，被调用元素嵌套在其中的元素。

## 操纵 DOM

最后，我们想改变节点。通常，我们希望将这些修改放在事件侦听器中，这样只有当用户与网页交互时(点击、鼠标悬停、按键)才会发生更改。例如，如果用户点击一个图像，我们可以简单地在这个`<img>`对象上调用`remove()`，它就会从网页上消失。

请记住，这些变化不会改变网页与一个简单的刷新一切都恢复正常。操纵 DOM 对象最常见的方法是简单地设置对象的 value 属性。试验所有的属性，并测试哪些属性可以被重新赋值。

[*更多内容看 plainenglish.io*](http://plainenglish.io/)