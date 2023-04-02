# 你应该知道的 6 个有用的纯 CSS 技巧

> 原文：<https://javascript.plainenglish.io/6-useful-pure-css-tips-that-you-should-know-647ccaff201e?source=collection_archive---------1----------------------->

## 你可能不知道的极其有用的 CSS 技巧

![](img/67b4a2683f0b0f814d9e76d0e93ab978.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

CSS 是一种很棒的样式表语言，它允许你设计网页的样式并使它们具有响应性。这是所有 web 开发人员必须知道的，因为每个网站或 web 应用程序都使用 CSS。

现在 CSS 进步了很多。不使用 JavaScript，你也可以用它创造一些很棒的东西。这就是为什么你需要知道一些 CSS 技巧，让你在你的项目中制作出令人惊叹的 UI。

在本文中，我们将向您展示一些有用的 CSS 技巧，您可以在接下来的项目中使用它们。所以让我们开始吧。

# 1.设置滚动条的样式

使用 CSS，你可以很容易地在你的网站上设置默认滚动条的样式。所以你可以让它看起来很棒。

为此，您需要使用属性`::scrollbar`和`::scrollbar-thumb`，就像我们在下面的代码示例中所做的那样:

```
body{
  height: 200vh;
}
**::-webkit-scrollbar**{
  width: 17px;
}
**::-webkit-scrollbar-thumb**{
  background: black;
}
```

正如你所看到的，我们为 Chrome 和 Safari 中的浏览器支持添加了`-webkit-`。我们还添加了我们的样式，使黑色滚动条的宽度更大。

您可以在下面的代码栏中查看:

Codepen by author.

# 2.设置选择的样式

当我们浏览网站或阅读博客时，我们经常用鼠标选择文本。但是好的一面是你可以在 CSS 中改变选择样式。

属性`::selection`允许您轻松更改所选文本的样式。

下面是代码示例:

```
**::selection{
  background: yellow;
  color: black;
}**
```

添加上面的样式表后，当您用鼠标选择文本时，它将具有黄色背景和黑色。

您可以用鼠标在下面的代码笔中选择文本，以查看结果:

Codepen by author.

# 3.平滑滚动

您可以使用 CSS 属性`scroll-behavior`将`html`用作选择器，以便在整个 HTML 页面上实现平滑滚动。

这里有一个例子:

```
html{
 **scroll-behavior: smooth;** }
```

点击链接查看下面的代码栏，查看页面如何在各部分之间平滑滚动:

Codepen by author.

# 4.纯 CSS 黑暗模式

你知道不使用 JavaScript 就可以很容易地给你的站点添加黑暗模式吗？我看到一些开发人员使用 CSS 变量来创建黑暗模式。但是有另一个很酷的技巧可以让你在没有 CSS 变量的情况下实现同样的事情。

因此，我们可以在类型为`checkbox`的输入上使用伪元素`::checked`来轻松地在暗模式和亮模式之间切换。

看看下面简单的 HTML 和 CSS 代码:

*HTML:*

```
<body>
    <input type="checkbox" id="checkbox">
    <div class="container">
      <h1>Hello World!</h1>
      <div class="div1">
        <p>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Doloribus, pariatur?</p>
      </div>
    </div>
</body>
```

*CSS:*

```
body{
    height: 100vh;
}.container{
    width: 100%;
    height: 100%;
    padding: 80px 20px;
    transition: .4s ease;
}/* When the checkbox is clicked */
**#checkbox:checked + .container{
  background: black;
  color: white;
}**
```

这只是一个简单的例子。你可以看看下面的代码笔:

Codepen by author.

如果你想知道更多关于使用`::checkbox`的黑暗模式的细节，请查看我下面的文章:

[](/dark-mode-switch-without-javascript-112e65e6a1e3) [## 无 JavaScript 的黑暗模式开关

### 我们来做一个没有 JavaScript，没有 CSS 变量的黑暗模式切换。

javascript.plainenglish.io](/dark-mode-switch-without-javascript-112e65e6a1e3) 

# 5.插入符号颜色

您还可以使用 CSS 更改文本输入中的插入符号颜色。属性`caret-color`允许你这样做。

这里有一个例子:

```
input{
 **caret-color: red;**
}
```

下面是检查它的代码笔:

Codepen by author.

# 6.圆锥梯度

CSS 的另一个很酷的地方是你可以创建漂亮的饼状图。CSS 函数`conic-gradient`允许你这样做。

下面是 CSS 代码示例:

```
div{
  width: 300px;
  height: 300px;
  border-radius: 50%;
  background: **conic-gradient(red 0% 20%, blue 20% 60%, black 60% 100%);**
}
```

您可以在下面的代码栏中查看:

Codepen by author.

# 结论

正如你所看到的，有很多很酷的事情，你可以只用纯 CSS 而不使用任何框架或库。这就是为什么 CSS 非常重要，尤其是对于前端开发者来说。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/es2021-logical-assignment-operators-in-javascript-c6a8290dc510) [## JavaScript 中的 ES2021 逻辑赋值运算符

### 您需要了解的新 ES12 逻辑赋值运算符。

javascript.plainenglish.io](/es2021-logical-assignment-operators-in-javascript-c6a8290dc510) 

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)