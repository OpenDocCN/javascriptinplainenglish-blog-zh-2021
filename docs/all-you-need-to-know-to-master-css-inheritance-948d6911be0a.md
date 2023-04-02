# 掌握 CSS 继承需要知道的一切

> 原文：<https://javascript.plainenglish.io/all-you-need-to-know-to-master-css-inheritance-948d6911be0a?source=collection_archive---------17----------------------->

## 通过示例了解初始化、继承、取消设置和恢复。

![](img/db705244b669bb1cadb38b60f0481325.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当您想要构建交互式用户界面时，级联样式表(CSS)是非常强大的。CSS 是很难掌握的，它包含了很多细节，这些细节只能通过构建和持续的练习来学习。

在这篇文章中，我们将学习 CSS 继承和它的一些基本特性，以了解它是如何工作的。系好安全带，打开代码编辑器，让我们学习一些其他东西。

让我们考虑一个实例，其中有一个 div，里面有一些 HTML 内容。默认情况下，div 上的显示总是内联的。嗯，根据 div 上给出的浏览器用户代理样式，不一定总是这样。包括 Chrome 在内的大多数浏览器都将 div 的默认用户代理样式设置为 block。要将它设置为初始值，我们需要将显示设置为 initial。

## **初始属性**

显示的初始值属性是内联的。所以，以下面给出的代码片段为例。我们可以看到，如果你检查开发人员控制台，你会发现，默认情况下，我们正在使用的 chrome 浏览器，在这种情况下，设置显示的值为阻止。这些是应用于元素的浏览器默认样式(浏览器的用户代理样式表)。

使用 display 属性的初始值，它将显示设置为 inline。根据默认的 CSS 规范，inline 是 display initial 的默认值属性。现在，我们可以将显示设置为初始，如果您查看网站，您会发现显示已设置为内联。

如果没有属性应用于元素以覆盖它们，则应用初始值。关于这方面的更多信息，你可以查看[链接](https://developer.mozilla.org.en-US/docs/web/CSS/display)

## **继承财产**

顾名思义，它使元素能够继承父元素的样式。大多数时候你会用到这个属性。举个例子，我们有一个 p 标签，它的父元素是一个 div。

```
<style>div {font-size: 3rem;}</style></head><body><div>CSS INHERIT<P>CSS IS AWESOME</P></div></body></html>
```

以上面显示的代码为例。如果在浏览器中启动它，您会发现 p 标记继承了其父 div 的字体大小，因此与 div 标记中的其他元素具有相同的字体。默认情况下，某些属性会被继承，而其他属性(如 border)则不会被继承。

如果我们希望父元素中的元素具有与其父元素相似的属性，我们必须将要继承的属性值设置为 inherit。这将确保它获得与为其对应的父元素指定的样式值相同的样式值。

类似地，甚至其他不适合继承的属性也可以通过简单地在属性上传递 inherit 值来强制继承其父属性的样式。

## **未设置属性**

未设置的属性与我们已经讨论过的非常相似。这是初始属性和继承属性的完美结合。

当我们将未设置的值传递给属性时，它将根据元素应用于 inherit 或 initial。当您希望将大多数元素的属性设置为 inherit on initial 时，Unset 很重要。尽管它不是最常用的。

## **恢复属性**

顾名思义，这个 value 属性用于恢复(回滚)浏览器中使用的默认样式——在大多数情况下是用户代理样式表。虽然不是很受欢迎，但如果你想回滚到浏览器的默认风格，你可以选择 revert 来完成这项工作。

## **最后的想法**

感谢您到目前为止阅读了这篇文章，我希望您在学习 CSS 继承和这种编程语言的超能力时发现它是有用的(只是开玩笑)。

谢谢你，如果你觉得这篇文章值得你花时间，请不要犹豫与他人分享。我的意思是也和你的敌人分享。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)