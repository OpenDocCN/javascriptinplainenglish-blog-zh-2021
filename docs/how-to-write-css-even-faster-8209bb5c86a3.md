# 如何更快地编写 CSS

> 原文：<https://javascript.plainenglish.io/how-to-write-css-even-faster-8209bb5c86a3?source=collection_archive---------17----------------------->

## Emmet 使用 CSS 的缩写

![](img/1b2cfb5c46e4b173f8b4fdcef3e86ebc.png)

Photo by [John Cameron](https://unsplash.com/@john_cameron?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在进行项目时，有经验的程序员倾向于寻找捷径来节省时间。他们似乎很匆忙，为了节省时间，他们换到了`i++`而不是`i = i + 1`。有许多可用的选项或[插件可以让你的 web 开发工作流程变得简单](https://sameerkatija.medium.com/make-your-web-development-workflow-smooth-with-these-5-vs-code-extensions-c394ab5ca19b)。埃米特就是其中之一。

Emmet 是一个文本编辑器的插件，它在一些缩写词的帮助下使编码高速进行。像在 Html 中我们写`html:5`我们会得到这个代码

这是 HTML，但你在这里学习如何更快地编写 CSS，而不是 HTML。不要担心，我会通过一些 CSS 的 Emmet 缩写来指导你，这将有助于你的工作流程更快更顺畅。那么，我们开始吧。

# Emmet for CSS

您可能认为 emmet 只对 HTML 有用，但事实并非如此。可以把 Emmet 和 CSS 一起用。Emmet 只为你提供 CSS 属性的快捷方式。例如，如果我们写`m0`，我们将得到`margin: 0;`，让我们探索其他一些常用的，可以帮助我们更快地编码。

# Emmet 的缩写

Emmet 附带了一堆快捷方式，比如`p`是`padding`的缩写、`w`是`width`、`h`是`height`的缩写、`m`是`margin.`的缩写。在开始使用 Emmet 之前，我们需要讨论一些常见的用例。

## CSS 单位

如果您键入带有 Emmet CSS 缩写的默认值，那么您将得到`px`作为默认单位。如果你想要一些其他单位，如 em，rem 或百分比，那么你必须使用别名

```
e → em
r → rem
p → %
x → ex
```

## 颜色值

Emmet 支持颜色，我们可以用它来编写颜色快捷方式。像`c#0`一样，生成的输出将是`color: #000000`。其他一些使用案例包括

```
#1 → #111111
#e0 → #e0e0e0
#fc0 → #ffcc00
```

## 分离器

当在一行中写很多属性时，我们使用`+`来区分属性。

# 结论

所以，我们可以看到 emmet 用这些快捷键让 CSS 编写变得超级简单。想想看，你可以用一条语句写五行。这不是很棒吗？如果您有兴趣了解更多信息，请查看此处的备忘单。