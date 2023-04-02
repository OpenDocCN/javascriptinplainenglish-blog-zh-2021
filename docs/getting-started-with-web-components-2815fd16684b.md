# Web 组件入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-web-components-2815fd16684b?source=collection_archive---------11----------------------->

![](img/fbeb9591fc1529967786ca4d96c9fea8.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你曾经使用过 ***React*** 的话，你会对 Web 组件很熟悉。它们是定制的、可复制的 HTML 片段，可以在代码的其他地方引用。

Web 组件是它们自己的 HTML 规范，所以你可能会惊讶于它们可以以独立的方式与纯 JavaScript 和 HTML 一起使用。让我们来看看如何做到这一点。

假设我们有一个在多个地方重复使用的状态栏项目。它的结构可能是这样的:

想象一下，必须将它粘贴到**多个位置**并保持它看起来总是一样的——如果我们某天改变了状态栏会怎么样？我们需要回到状态栏出现的所有地方，并更新它们！ **Web 组件**允许你在多个地方引用这段 HTML，并给它一个唯一的标签，即:

***我们怎么做呢？*** 让我们来看看如何制作自己的 web 组件，有多简单。

# 步骤 1 — JavaScript

是的，你猜对了。如果你想做 web 组件，你需要使用 JavaScript。让我们快速看一下如何创建一个非常简单的 DOM 元素，我们称之为“段落”。

它的输出将是一个包含单词“Hello”的段落。Web 组件依赖于类结构。我们在这里使用`constructor()`来表示标签加载时会发生什么。

# 其他功能

除了构造函数，我们还可以向类中添加其他函数，比如当 DOM 元素被追加到页面时触发的`connectedCallback()`，以及当元素的属性改变时触发的`attributeChangedCallback()`，这给了我们一些灵活性:

# 步骤 2 —扩展功能

现在我们有办法创建一个简单的元素，给它附加回调事件，给属性变化附加事件，让我们考虑 CSS。当制作一个独立的、可克隆的 web 组件时，我们希望它在多个地方看起来物理上是相同的。为此，它需要自己的自定义 CSS。我们如何将 CSS 添加到 web 组件中？

为此，我们需要使用一种叫做影子 DOM 的东西。这些基本上是仅附加到一个特定项目上的项目。我们可以通过启用 shadow DOM 将它用于 web 组件，并将 CSS 附加到它上面。

## 添加 CSS

在上面的例子中，任何一个`alpha-paragraph`元素都有一个段落是`red`，字体大小是`1.25rem`。

所有在`alpha-paragraph`之外的段落都不会是红色的，所以你可以独立地设计你的其他 CSS 样式。

# 步骤 3 —与模板标签结合

我们可以使用 HTML 标签，而不是将 web 组件硬编码成 Javascript。HTML 有两个标签我们可以在这里使用，`template`和`slot`。

模板标签指的是整个 web 组件，而槽是模板的一小部分，可以修改。模板标记的示例如下所示:

第二行的槽指的是我们可以改变的东西。在我看来，我们并不真的需要使用模板标签，但是槽是有用的。我们可以通过改变 innerHTML 来更新我们的`alpha-paragraph`,让它有一个 slot:

然后，我们可以使用 HTML 中的“slot”属性，用我们自己的自定义元素来替换该 slot。在下面的示例中，整个槽被替换为包含文本“自定义文本”的段落元素。

# 第 4 步—属性

因为所有的 HTML 元素都可以有属性，所以我们可以使用`getAttribute`函数来访问它们。因此，我们可以轻松地重新编写代码来定制颜色:

通过将其全部放入我们的 Javascript 中，我们确保可以轻松地将这个 web 组件导入到其他地方。我们最终的 web 组件的演示如下所示:

就是这样。希望这篇文章对你有用，感谢你的阅读。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)