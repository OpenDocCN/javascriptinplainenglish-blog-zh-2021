# 在没有任何库或实用程序的情况下实现暗模式

> 原文：<https://javascript.plainenglish.io/implement-dark-mode-without-any-library-or-utility-cf2271af5837?source=collection_archive---------17----------------------->

## 你不会相信它有多简单

![](img/578e525c6ab22eea861608f9b45e4055.png)

Photo by [Quinton Coetzee](https://unsplash.com/@quincoetzee) on [Unsplash](https://unsplash.com/photos/_fHzsyyDcuQ)

## 介绍

黑暗模式正在成为当今的一种趋势。当苹果在最新的 iOS 中采用黑暗模式时，这种趋势就出现了，随后安卓手机也出现了。暗模式是当今网站必须具备的功能，我访问的几乎每个网站都有暗模式功能。但是仍然有些人不知道如何实现正确的方法，所以有时他们更喜欢安装一个新的库。今天，我想向你展示在没有任何库的情况下实现暗模式是多么简单。

## 深入研究代码示例

Example HTML content

这只是一个示例正文 html。我在页面顶部放置了一个复选框来切换暗模式功能。我用“ [onClick](https://www.w3schools.com/jsref/event_onclick.asp) ”作为切换黑暗模式的例子。对于每一个内容，我都给出了这些 CSS 类名，以帮助您区分并看到结果。

Example CSS

魔术和小窍门都出现在这些 CSS 文件中。您可以看到上面我使用了[:根选择器](https://developer.mozilla.org/en-US/docs/Web/CSS/:root)、 [CSS 变量](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)和[数据属性](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes)。[:根选择器](https://developer.mozilla.org/en-US/docs/Web/CSS/:root)匹配文档的根元素。它对于声明全局 CSS 变量非常有用。HTML5 数据属性是 HTML5 的一个特性，允许我们在 DOM 上存储额外的信息。

首先，在:根选择器中，我将所有默认的(灯光模式)背景颜色和文本颜色定义到一个变量中。之后，我还使用数据属性创建了新的 CSS 选择器。我给的名字是主题，价值是黑暗的。在选择器中，我定义了黑暗模式的所有背景颜色和文本颜色。

最后，我把所有的文本和背景颜色变量写到 CSS 类中，我希望当我切换暗模式时，它们会改变。

Example Js

最后，在 JavaScript 代码中，首先，默认情况下，我将“current 血红素”变量初始化为“light ”,然后我得到一个复选框，信息和主体 DOM，为 DOM 操作做准备。

当您切换复选框 DOM 时，会调用“更改主题”功能。基本上，这个函数用于切换“当前主题”并设置正文标签中的数据属性。切换后，身体应该如下所示。

```
<body data-theme="dark"></body>
```

然后 CSS 将自动覆盖我们在中定义的默认颜色变量:根到[data-theme="dark"]选择器。

## 演示示例

Codepen Demo

[Github 源代码链接](https://github.com/hanssagita/native-darkmode-example)

## 额外提示

你可以用[本地存储](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)保存用户偏好，这样当用户第二次访问你的网站时，主题会自动调整到用户最后一次选择的时候。

```
// define localStorage key
const localStorageThemeKey = "localStorageThemeKey"// Getting the currentTheme from localStorage, when the localStorage return undefined will automatically set to light
const getCurrentTheme = 
localStorage.getItem(localStorageThemeKey) || "light"// Save user input to the localStorage with localStorage key and currentTheme right now
localStorage.setItem(localStorageThemeKey, currentTheme);
```

## 结论

黑暗模式非常简单，你不需要一个库来实现它。

就这样，如果你觉得这篇文章有帮助，请在评论中告诉我们。也可以在[中](https://medium.com/@hanssagita)和 [LinkedIn](https://www.linkedin.com/in/hans-sagita/) 上关注我