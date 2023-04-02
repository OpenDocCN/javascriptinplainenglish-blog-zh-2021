# 理解“样式化组件”的奇怪语法

> 原文：<https://javascript.plainenglish.io/understanding-the-weird-syntax-of-styled-components-405a36ffce23?source=collection_archive---------17----------------------->

![](img/8aebf403c4ff42592d50caa9587108da.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当我们第一次尝试学习时，大多数人都会对`styled-components`的语法感到困惑。当我第一次看到它时，我有许多疑问:它到底是如何工作的？它使用了一些我不知道的新的 JavaScript 实体吗？例如，让我们制作一个红色文本的按钮。

```
const Button = styled.button`
    color : red;
`
```

这里的“styled.button”到底是什么？是新的 JavaScript 实体吗？原来“styled.button”只不过是一个函数。当我发现这是一个函数时，我彻底糊涂了。它是如何工作的？就在那时，我发现了[标记的模板文字](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#tagged_templates)

样式化的组件使用标记的模板文字。在 JavaScript 中，当我们将模板文字作为参数传递给函数时，可以省略括号。这个特性被称为标记模板文字。

例如:

```
function print(string){ console.log(string.toString())
}//normal function call
print("Hello World")
// logs "Hello World" // function call with tagged templates
print`Hello World`
// logs "Hello World"
```

这两个函数调用是相同的，但语法不同。第二个是我们所说的标记模板文字。

# 结论

这就是样式化组件的工作方式，一旦我们理解了标记模板，就很容易理解了。*我没有深入标记模板，因为这是一个很大的话题，但这种理解应该足以处理样式化组件。*

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)