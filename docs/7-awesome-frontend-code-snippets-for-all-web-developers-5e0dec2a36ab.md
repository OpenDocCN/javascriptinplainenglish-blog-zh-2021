# 面向所有 Web 开发人员的 7 个出色的前端代码片段

> 原文：<https://javascript.plainenglish.io/7-awesome-frontend-code-snippets-for-all-web-developers-5e0dec2a36ab?source=collection_archive---------5----------------------->

## 前端 web 开发中有用的代码片段列表。

![](img/1a179c01176d53139edacb7cca19d111.png)

Photo by [Nicole Wolf](https://unsplash.com/@joeel56?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

就软件开发或一般编程而言，前端开发是最受欢迎的领域之一。现在很多人都在追求前端开发的职业生涯。这是技术领域最好的职业之一，因为它让你更有创造力，用代码把想法变成现实。你只需要对你所做的事情有激情和热爱。

前端开发每年都在进步。有很多技术、库和工具可以用来构建用户界面和开发 web 应用程序。看起来前端开发人员每天都有很多工作要做。然而，也有很多工具和方法可以让你的生活更轻松。

在本文中，我想与您分享一些有用的代码片段，它们可以让您的 web 开发人员的生活变得更加轻松。所以让我们开始吧。

# 1.原生 HTML 折叠

是的，你可以只用 HTML 创建一个很棒的手风琴。标签`<details>`和`<summary>`允许你这样做。

看看下面的代码示例:

```
<div class="container">
  **<details>**
    **<summary>**
      HTML stands for?
    **</summary>** <p>HTML stands for hyper text markup language.</p>
  **</details>**
</div>
```

*输出:*

Created by the author using Codepen(embedded iframe).

如您所见，在标签细节中，您放置了问题及其答案。问题或标题是使用标签`<summary>`创建的，答案在摘要标签之后。您可以使用上面相同的代码片段创建多个问题及其答案。

# 2.使用 HTML 延迟加载图像

属性`loading`允许我们推迟图像加载，直到我们滚动到它，以提高性能和页面加载时间。

为此，您只需要给属性(`loading=”lazy"`)赋值`lazy`。

这里有一个例子:

```
<img src='imageSrc.jpg' **loading='lazy'** alt='image description'>
```

# 3.将 div 居中

您可以使用 CSS flexbox 属性轻松地将子 div 放在父 div 的中心。您只需在父元素中使用 flexbox 属性。

下面是代码示例:

```
.parent{
  **display: flex;
  align-items: center;
  justify-content: center;**
  height: 100vh;
}
```

如果你不熟悉 CSS flexbox，你可以看看我下面的文章:

[](/css-flexbox-explained-with-examples-85efa38e4770) [## CSS Flexbox 举例说明

### 通过实例了解 CSS flexbox。

javascript.plainenglish.io](/css-flexbox-explained-with-examples-85efa38e4770) 

# 4.自动响应网格布局

假设您有一个包含大量图像或博客文章的网格布局。要轻松地使这种布局在所有屏幕尺寸下自动响应，您可以使用一些非常棒的 CSS 网格功能。

CSS 网格函数`repeat()`和`minmax()`允许你这样做。看看下面的例子:

```
.grid-layout{
  display: grid;
  **grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));**
  grid-gap: 10px;
}
```

通过在我们的网格布局中使用上面的代码片段，所有最小宽度为 250px 的网格项将自动适合所有的屏幕尺寸。例如，如果您正在创建自己的博客或画廊，这是一个非常有用的功能。

你可以通过调整屏幕来查看这个[代码笔](https://codepen.io/MehdiAoussiad/pen/zYKyyYY) *(外部链接)*的变化。

# 5.将文本复制到剪贴板

当谈到将文本复制到剪贴板时，有一个 JavaScript 片段被许多开发人员使用。这是导航器对象。在大多数情况下，您需要一个按钮，允许用户将文本复制到剪贴板。

下面是一个代码示例:

```
function CopyText() {
  // select the text element. 
  let text = document.getElementById("myText");

  // select text.
  **text.select();
  text.setSelectionRange(0, 99999);**

   // Copying the text inside the text field
  **navigator.clipboard.writeText(text.value);**

  //if you want an a copy alert.
  alert("Copied the text: " + text.value);
}
```

现在，每当您想在单击按钮后复制文本时，您可以选择文本元素，并将上面的复制函数添加到按钮的 click 事件处理程序中。

# 6.滚动到顶部

如今，大多数网站和网络应用程序都有一个按钮，允许用户轻松地滚动到顶部。为此，您只需要使用方法`scrollTo(x, y)`并将 x 和 y 设置为 0。

这里有一个例子:

```
const ScrollTop = () => **window.scrollTo(0, 0)**;

ScrollTop();
```

# 7.轻松创建颜色选择器

您可以轻松地创建一个可怕的颜色选择器使用原生 HTML 没有任何 CSS 或 JavaScript。您只需要使用输入标签并赋予它一种颜色。

下面是代码示例:

```
<input type="color" value="#000">
```

*输出:*

Created by the author using Codepen(embedded iframe).

# 结论

正如您在上面的列表中所看到的，这些是您可以在前端开发中使用的一些有用且重要的代码片段。无论您是前端开发人员还是 web 开发人员，在某些情况下您总是需要使用这些代码片段。

*感谢您阅读这篇文章。此外，如果你发现我的内容有用，而你不是一个媒体成员，你可以抓住你的媒体成员* [*这里*](https://mehdiouss.medium.com/membership) *(媒体推荐链接)获得所有内容的无限访问和支持我们作为作家。*

**延伸阅读:**

[](/6-awesome-sites-for-all-front-end-developers-d15835790796) [## 面向所有前端开发人员的 6 个优秀网站

### 你可能不知道的有用网站列表。

javascript.plainenglish.io](/6-awesome-sites-for-all-front-end-developers-d15835790796) [](/7-useful-javascript-code-snippets-for-solving-coding-problems-c146e768bb41) [## 解决编码问题的 7 个有用的 JavaScript 代码片段

### 您经常需要使用的 JavaScript 代码片段。

javascript.plainenglish.io](/7-useful-javascript-code-snippets-for-solving-coding-problems-c146e768bb41) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)