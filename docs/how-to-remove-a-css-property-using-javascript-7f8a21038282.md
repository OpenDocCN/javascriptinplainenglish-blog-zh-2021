# 如何使用 JavaScript 移除 CSS 属性？

> 原文：<https://javascript.plainenglish.io/how-to-remove-a-css-property-using-javascript-7f8a21038282?source=collection_archive---------5----------------------->

![](img/ab5e96801cc6c226272b73228d68c075.png)

Photo by [Tierra Mallorca](https://unsplash.com/@tierramallorca?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望使用 JavaScript 从 HTML 元素中移除 CSS 属性。

在本文中，我们将了解如何使用 JavaScript 删除 CSS 属性。

# 使用 style.removeProperty 方法

我们可以使用`removeProperty`方法从元素中移除 CSS 属性。

例如，如果我们有下面的 HTML:

```
<div style='background-color: green'>
  hello
</div>
```

我们可以通过编写以下代码来删除`background-color`属性:

```
const el = document.querySelector('div')
el.style.removeProperty('background-color');
```

# 将 CSS 属性设置为空字符串

从 HTML 元素中移除 CSS 属性的另一种方法是将其值设置为空字符串。

例如，我们可以写:

```
const el = document.querySelector('div')
el.style.backgroundColor = ''
```

移除 CSS `background-color`属性的值。

# 结论

我们可以通过设置一个空字符串或者调用`removeProperty`方法来从一个对象中移除 CSS 属性。