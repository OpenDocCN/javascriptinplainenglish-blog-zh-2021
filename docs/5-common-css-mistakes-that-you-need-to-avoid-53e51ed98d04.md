# 你需要避免的 5 个常见 CSS 错误

> 原文：<https://javascript.plainenglish.io/5-common-css-mistakes-that-you-need-to-avoid-53e51ed98d04?source=collection_archive---------4----------------------->

## 避免这些 CSS 错误来改进您的代码和样式。

![](img/9ba50667b8750ae9d38815b8bd3e2ddf.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

CSS 是每一个 web 开发人员都必须知道的语言，以便设计 web 页面的样式并使它们具有响应性。我无法想象网页不使用 CSS 会是什么样子。使用这种令人惊叹的样式表语言，您可以做很多很酷的事情。

你只需要有点创造性，避免代码中的错误。在 CSS 中很容易出错，因为你必须对网页上的几乎每个元素进行样式化。

这就是为什么在这篇文章中，我们将涵盖一些作为 web 开发人员需要避免的常见 CSS 错误。让我们开始吧。

# 1.不使用相对单位

我也犯过的一个常见错误是，我看到许多新开发人员都犯过，他们硬编码 PX 单位，而不是只使用相对单位(`rem`、`%`、`em`……)。

相对单位确保布局根据用户屏幕进行缩放。所以尽可能使用它们，避免在代码中到处使用 px 单位。

*坏道:*

```
/* wrong */element{
 font-size: **18px**;
 margin: **10px**;
 line-height: **15px**;
}
```

*好办法:*

```
/* right */element{
 font-size: **1.2rem**;
 margin: **0.5rem**;
 line-height: **1.3em**;
}
```

# 2.无 CSS 重置

每个 web 浏览器都有自己的默认样式。因此，当网页不包含 CSS 时，浏览器会为文本、填充、边距等添加一些基本的默认样式。

每个浏览器都有独特的默认风格。这就是为什么通过添加 CSS 重置来重置这些默认样式总是更好的原因。然而，许多开发人员并不这样做。通过添加 CSS 重置来避免这个错误。

您可以通过使用通用选择器`*`重置边距、填充、框大小和文本字体来实现。

像这样:

```
*{
 padding: **0**;
 margin: **0**;
 box-sizing: **border-box**;
 font-family: "your preferd font here"**;** }
```

# 3.重复代码

很多开发人员在谈到 CSS 时会重复自己的话。这是一个糟糕的做法，因为你需要减少代码，使其具有高性能并易于管理。

因此，总是寻找减少 CSS 和避免重复代码的方法。

这里有一个例子:

*不良做法:*

```
/* wrong */.container {
    background-color: #000;
    border-radius: 0.5rem;
}

.sidebar {
    background-color: #000;
    border-radius: 0.5rem;
}
```

*良好实践:*

```
/* right */.container, .sidebar {
    background-color: #000;
    border-radius: 0.5rem;
}
```

# 4.不使用人手短缺

同样在 CSS 中，有一些简写，你可以用它们来编写更少的 CSS 代码。但是许多开发人员并不使用这些人手，或者他们甚至不知道这些人手。嗯，我也是那些开发者之一，我不打算说谎。

以下是一些例子:

*不使用速记(不好的方式):*

```
element{ **background-image:** url(file.png);
 **background-repeat**: no-repeat;
 **background-position:** center;
}
```

*使用速记(好方法):*

```
element{ **background: url(file.png) no-repeat center;
}**
```

这是另一个例子:

```
/* without shorthand */
element{ **font-family:** Helvetica;
 **font-size:** 1rem;
 **font-weight:** bold;
}/* using a shorthand */
element{
 **font: bold 1rem Helvetica;
}**
```

如你所见，短工减少了 CSS 代码。这就是为什么你需要尽可能多地使用它们。

# 5.使用颜色名称

不要用`red`、`blue`等颜色名称。相反，我建议使用十六进制值的颜色。

为什么？原因很简单，当你使用像`red`这样的颜色名称时，这种颜色在所有浏览器中看起来并不完全一样。通过使用颜色名称`red`，你允许浏览器显示它认为红色的东西。

这就是为什么建议使用十六进制颜色来更具体地选择你的颜色，以便在所有浏览器中看起来都一样。

*坏道:*

```
/* wrong */
element{
 color: **blue**; **}**
```

*好办法:*

```
/* correct */
element{
 color: **#2596be**; **}**
```

# 结论

如你所见，这些是你作为一个 web 开发者需要避免的 CSS 错误。我也犯了一些这样的错误。所以我想和你分享。

感谢您阅读这篇文章。希望你觉得有用。

**延伸阅读:**

[](/the-ultimate-css-flexbox-cheat-sheet-with-examples-7a62dce086dc) [## 终极 CSS Flexbox 备忘单及示例

### 用通俗易懂的例子学习 CSS flexbox。

javascript.plainenglish.io](/the-ultimate-css-flexbox-cheat-sheet-with-examples-7a62dce086dc) [](/8-extremely-useful-vscode-extensions-for-reactjs-developers-9b0da7de4f47) [## 8 个对 React 开发人员非常有用的 VSCode 扩展

### 每个 React 开发人员必备的 VSCode 扩展列表。

javascript.plainenglish.io](/8-extremely-useful-vscode-extensions-for-reactjs-developers-9b0da7de4f47) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)