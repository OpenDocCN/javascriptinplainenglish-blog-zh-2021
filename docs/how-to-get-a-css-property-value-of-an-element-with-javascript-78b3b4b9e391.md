# 如何用 JavaScript 获取元素的 CSS 属性值

> 原文：<https://javascript.plainenglish.io/how-to-get-a-css-property-value-of-an-element-with-javascript-78b3b4b9e391?source=collection_archive---------14----------------------->

![](img/9ebf3824da26865f7200ddc480d9b101.png)

Photo by [Joshua Chun](https://unsplash.com/@joshuachun?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想用 JavaScript 获得一个元素的 CSS 属性值。

在本文中，我们将研究如何用 JavaScript 获取元素的 CSS 属性值。

# 使用 window.getComputedStyle 方法

我们可以使用`window,getComputedStyle`方法来获取元素的 CSS 样式。

例如，如果我们有下面的 HTML:

```
<div style='height: 300px; overflow-y: auto'></div>
```

然后我们可以编写下面的 JavaScript:

```
const div = document.querySelector('div')
for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  div.appendChild(p)
}const style = window.getComputedStyle(div);
const height = style.getPropertyValue('height');
console.log(height)
```

向 div 添加一些内容。

我们使用`for`循环将 100 个`p`元素添加到带有`document.createElement`的 div 中。

然后我们设置每个元素的`textContent`来添加一些内容。

然后我们调用`div.appendChild`来添加`p`元素作为 div 的子元素。

接下来，我们用`div`调用`window.getComputedStyle`来获得一个`style`对象。

然后我们可以用下面的方法得到`height`属性:

```
const height = style.getPropertyValue('height');
```

而`height`是`'300px'`，因为我们在 HTML 中是这样设置的。

# 使用元素的 computedStyleMap 方法

此外，我们可以使用元素自带的`computedStyleMap`方法来获取应用于元素的样式。

例如，我们有以下 HTML:

```
<div style='height: 300px; overflow-y: auto'></div>
```

我们可以编写下面的 JavaScript:

```
const div = document.querySelector('div')
for (let i = 1; i <= 100; i++) {
  const p = document.createElement('p')
  p.textContent = i
  div.appendChild(p)
}const style = div.computedStyleMap();
const height = style.get('height');
console.log(height)
```

最后 3 行以上的都和之前一样。

然后我们调用`div.computedStyleMap`来获得一个`style`对象，我们可以用它来获得样式。

然后我们有:

```
const height = style.get('height');
```

获取 div 的 CSS `height`属性值。

这个时间`height`应该是:

```
{value: 300, unit: "px"}
```

在返回的对象中，值和单位是独立的属性。

# 结论

有几种方法可以用来通过 JavaScript 从元素中获取 CSS 属性。

*更多内容请看*[***plain English . io***](http://plainenglish.io)