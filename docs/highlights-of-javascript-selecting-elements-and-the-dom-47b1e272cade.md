# JavaScript 亮点——选择元素和 DOM

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-selecting-elements-and-the-dom-47b1e272cade?source=collection_archive---------14----------------------->

![](img/ecfb0d7ee179e1df57553e6bbdb36a03.png)

Photo by [Helena Hertz](https://unsplash.com/@imperiumnordique?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 使用 querySelectorAll 通过标记名定位所有元素

`document.querySelectorAll`方法让我们用给定的选择器获取所有元素。

因此，要获得具有给定标记名的所有元素，我们可以编写以下 HTML:

```
<p>foo.</p>
<p>bar.</p>
<p>baz.</p>
```

然后我们可以得到所有的这些，并通过编写来设计它们的样式:

```
const pars = document.querySelectorAll('p')
for (const p of pars) {
  p.style.fontFamily = "Verdana, Geneva, sans-serif";
}
```

我们用`document.querySelectorAll`得到所有的`p`元素。

然后我们用 for-of 循环遍历每一项，并设置`style.fontFamily`属性来设置字体系列。

# 通过标记名定位一些元素

我们可以用`document.querySelectorAll`方法通过标签名来定位一些元素，因为它将任何选择器字符串作为参数。

例如，如果我们有下面的 HTML 表:

```
<table>
  <tr>
    <td>foo</td>
    <td>bar</td>
    <td>baz</td>
  </tr>
</table>
```

并且我们想得到表中所有的`td`元素，我们可以写:

```
const tds = document.querySelectorAll('table td')
for (const t of tds) {
  t.style.backgroundColor = "pink";
}
```

我们用`table td`选择器获取`table`元素中的`td`元素。

然后我们循环遍历`td`元素，并将`backgroundColor`设置为`'pink'`。

# 大教堂

DOM 代表文档对象模型。这是浏览器用 JavaScript 表示 HTML 元素的方式。

HTML 元素在 DOM 中被组织成一个树形结构。

每个级别都由缩进表示。

例如，如果我们有:

```
<html> <head>
    <title>
      Simple document
    </title>
  </head> <body>
    <p>
      hello world
    </p>
  </body></html>
```

那么`html`元素就是树的根。

`head`和`body`为第二级。

`title`和`p`元素位于第三层。

最顶层的元素是`document`对象。

因此`html`元素是`head`和`body`元素的父元素。

`title`元素是`head`元素的子元素。

并且`p`元素是`body`元素的子元素。

我们可以用之前用过的 DOM 方法找到子元素，比如`querySelector`、`querySelectorAll`、`getElementById`和`getElementByTagName`。

例如，如果我们有以下 HTML:

```
<html><head>
    <title>
      Simple document
    </title>
  </head> <body>
    <div id="weather">
      <p>Today is sunny.</p>
      <p>Yesterday is rainy.</p>
    </div>
    <div id="density">
      <p>City is crowded.</p>
      <p>Desert is sparse.</p>
    </div>
  </body>  
</html>
```

然后，如果我们想得到“今天是晴天”的文本，我们可以写:

```
const sunny = document.querySelector('#weather p');
console.log(sunny.innerHTML)
```

我们使用带有`querySelector`方法的`#weather p`选择器从 ID 为`weather`的 div 中获取第一个 p 元素。

然后我们用`innerHTML`属性获取它的内容。

# 结论

我们可以用`document`方法得到元素。

HTML 元素在浏览器中用 DOM 建模。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**