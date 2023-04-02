# “currentColor”:面向开发者的 CSS Hack

> 原文：<https://javascript.plainenglish.io/currentcolor-css-hack-for-developers-50c4755a138e?source=collection_archive---------15----------------------->

## 开发人员必须知道 CSS 功能

本文重点介绍 CSS 中的特性**“current color”。这是一个很少使用的高效有趣的 CSS 功能。让我们寻找“currentColor”的用例场景**

![](img/45e9a31ed483fa23bcbaf34c50135bcf.png)

Working with Css and currentColor Property

## 为什么使用“currentColor”属性

属性用于引用应用它的元素的当前“颜色”。它采用可以应用于其他属性的当前颜色的引用。我们不需要任何预处理程序。

让我们借助一个例子来理解这一点:

在上面的 CSS 中，我们让边框颜色等于文本颜色。我们使用属性“currentColor ”,它告诉浏览器解析器提取应用于 id 为“root”的元素上的文本的当前颜色，并在“border”上应用相同的颜色。

# “当前颜色”的级联效果

[https://gist.github.com/Mayankgupta688/3005a47c13d368616237a8d4ed9b91c9](https://gist.github.com/Mayankgupta688/3005a47c13d368616237a8d4ed9b91c9)

在上面的场景中，没有对 id 为“root”的元素应用颜色属性。在这种情况下，应用于 body 的颜色将应用于 id 为“root”的元素，而“currentColor”属性将从“body”标记中提取颜色。应用于元素的有效颜色将与属性“currentColor”所引用的颜色相同。

**在使用该属性之前，请寻找该属性的浏览器支持。*

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)