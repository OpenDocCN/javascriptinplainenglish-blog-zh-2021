# 带有变量的现代可扩展 CSS 框架

> 原文：<https://javascript.plainenglish.io/modern-scalable-css-framework-with-variables-3aaf6856c105?source=collection_archive---------9----------------------->

![](img/364e95a970f2e8d984e971f0aa278192.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

一天，当我醒来时，我发现 CSS 世界似乎也很有趣。当我回来拿起关于 CSS 框架的最新书籍时，我发现他们仍然经常谈论 SASS/SCSS，这让我非常惊讶。

尽管它们仍然有效和流行，但是如果你打开任何一个现代的网站，你会看到另一种制作模块化样式的方式，这就是所谓的 CSS 变量。如果您想直接获取文档，请在此处阅读更多[https://developer . Mozilla . org/en-US/docs/Web/CSS/use _ CSS _ custom _ properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties#basic_usage)。我不怪你，*信不信由你，这些天的文件在某些情况下比一本书要好。*

## 按比例增加

这个想法很简单。您可以为站点定义一个变量:

```
:root {
  --bg-color: brown;
}
```

上面的语法都不好看，包括`root`的`:`和变量`bg-color`的`—` 。当你第一次看到它的时候，你可能会把它当作一些系统级的信息，而忽略它。

事实证明，除了丑陋的外表之外，它们还非常有用。您可以做的第一件事是让另一个元素在下面引用变量:

```
h1 {
  background: var(--bg-color);
}
```

就这样。顺便说一下，这是支持在浏览器，而不是任何编译系统。

另外，您对可扩展的 CSS 模块系统还有什么要求？哦，你可能会想，变量是为整个范围定义的，所以不太具体。

事实上，您可以将定义移动到一个元素，而不是`:root`:

```
element {
  --bg-color: red;
}
```

这意味着，变量有一个作用域！天哪，这是件大事。一个包含文件夹的文件系统比一个简单的文件列表强大十倍。我们都知道，只要您不滥用文件系统，它就能很好地扩展。

你可以用这个简单的例子玩一会儿。

## java 描述语言

对于经常使用 JavaScript 的人来说，我们通常希望访问 JavaScript 中的 UI 变量来应用或激活样式。有了 CSS 变量，我们甚至可以在运行时抓住它:

```
const el = document.getElementById('title')
const style = window.getComputedStyle(el)
console.log(style.getPropertyValue('--bg-color'))
```

当然，这并不新鲜。您可以通过查询元素来获得运行时的任何元素信息。但是，因为 CSS 变量是在文档中正式定义的，所以我们可以将其视为变量定义的来源。如果您不想在两个地方重复定义，您可以从现在开始依赖 CSS 变量。这只是为我们打开的另一扇门。

此外，我们不仅可以将这些变量读入 JavaScript，还可以动态设置这些变量。

```
el.style.setProperty('--bg-color', 'blue')
```

## 安全

从使用的角度来看，这对开发者和用户来说都很容易，因为如果你对网站的某些风格不满意，你可以在浏览器中动态地改变这个变量。你甚至不需要黑它，因为开箱即用，它允许一个非技术人员“黑”它。

另一方面，旧的方法传输变量，所以你不能在浏览器上得到原始变量。如果用户需要改变一种风格，他必须找到那个元素。因此，从安全的角度来看，新的方式可能太容易被其他人愚弄的风格。所以好与坏，这是需要注意的。可以说，风格在大多数时候不是很重要的东西。

## 结论

简而言之，CSS 变量实际上是一个 CSS 框架的可伸缩解决方案。因此，由于浏览器的支持，尝试一下您的新开发工作，甚至将其融入现有的项目中。

*更多内容看*[***plain English . io***](http://plainenglish.io/)