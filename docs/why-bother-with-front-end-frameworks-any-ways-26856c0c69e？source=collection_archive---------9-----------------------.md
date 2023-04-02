# 为什么要为前端框架费心呢？

> 原文：<https://javascript.plainenglish.io/why-bother-with-front-end-frameworks-any-ways-26856c0c69e?source=collection_archive---------9----------------------->

![](img/035c2145be1ebfa38fea512b762220e0.png)

Photo by [Djordje Petrovic](https://www.pexels.com/@djordje-petrovic-590080?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/man-sitting-on-chair-2102413/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

我学完了 JavaScript。我已经了解了一些 HTML 和 CSS。是时候学习前端框架了。耶！但是……为什么呢？

蟋蟀！因为现在每个人都在这么做。我需要学习它们才能在这个行业找到工作。

这是我开始学习 React 的动力。我不知道人们说 React 有很好的工具是什么意思；是**快；****虚拟 DOM** 、**条块化**、**路由、**等等。

毫不夸张地说，我有一些想法。但是不断听到类似于**状态**、**成分**、**路由**等等的流行语，并没有在寻找动力的旅途上有所帮助。

我不是应该在学习了框架之后再学习它们吗？但是如果我必须只知道这些单词，我为什么要费心去学习框架呢？如果不学习这个框架，我怎么能真正理解这些单词的意思或者它们是如何工作的呢？

这就是我面临的困境。无论如何，我只是读了 React [文档](https://reactjs.org/docs/getting-started.html)(不完全，但和我理解的一样多)。在研究了一点之后，我终于对我为什么学习 React 有了一个更好的想法。有些人会说，这很讽刺。

我想这可能是许多程序员第一次遇到前端框架时面临的问题。这就是这篇文章的目的，分享我的发现。

![](img/74432f2a8e2bdda0108538828a0fbdf8.png)

Photo by [Ashkan Forouzani](https://unsplash.com/@ashkfor121?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**web 在框架之前和之后是如何工作的？**

在不涉及太多细节的情况下，让我们分析一下网站是如何运作的。您在浏览器中键入一个 URL。浏览器通过网络结构向服务器发送请求。如果服务器发现请求是合理的，它会尝试返回一个资源。

这些资源包括但不限于图片、HTML、CSS 和 JavaScript 文件。然后，您的浏览器读取 HTML，绘制布局，应用 CSS，并通过其 JavaScript 引擎执行 JavaScript。

现在，让我们举一个例子。说我们的网址是[这个](https://technext.github.io/news/index.html)网站我是从[这里](https://themewagon.com/)(*非赞助)。我们将用这个网站作为讨论我们想法的样本。首先，您可以在浏览器中键入 URL(或单击链接)，服务器会返回第一批资源。

![](img/6d180dd2d99a587cd47c97df10f51028.png)

What you type on the URL

然后，您的浏览器将呈现它们，您将看到如下所示的内容。

![](img/6a0e10a5d0400364b5ce2a8c8b3d92b0.png)

The home page, where the anchor for the about page is boxed

太好了，现在你在主页上。但是，假设您想使用某个锚链接转到另一个页面，那么您单击了 about 链接。然后浏览器花了一些时间(数量取决于你的互联网)加载了一个新的页面。新页面如下图所示。

![](img/411ec9e4c37588bd1200c1bbacfb447f.png)![](img/89b8421e16d2967c15193e63f39f343a.png)

如果你看到下面的两个页面，有一些常见的 HTML 元素，就像包在绿色盒子里的那些。他们一点都没变。请记住这一点，因为我们将在后面详细讨论。

![](img/f90e5e0632f6eb3e7fdf56683959533b.png)

那么，当你点击“关于”链接时发生了什么？
如果你仔细看地址栏，网址已经从[https://technext.github.io/news/index.html](https://technext.github.io/news/index.html)变成了[https://technext.github.io/news/about.html](https://technext.github.io/news/about.html)。

这个变化是对你按下链接的回应。您让浏览器向服务器发送了一个额外的请求。根据同样的原则，服务器用新的资源和新的页面进行响应。我们称之为客户端-服务器架构。在这种架构中，每一次交互都依赖于你的网速。这有它的警告。

**1。如果你想返回主页，你需要向服务器发送一个新的请求，即使你已经访问过那个页面。如果用户的网络速度很慢，因为他们必须等待来自服务器的资源，这可能会让他们很烦。如果我们在浏览器上存储每个页面，或者在第一次请求时一次发送所有页面，就可以解决这个问题。**

**2。**如果您的应用程序是一个交互式应用程序，您可能需要响应太多的用户输入，如果您必须联系服务器来处理每个交互，您可能不会给用户带来流畅的体验，因为在每个请求-响应周期中都有延迟。

**3。**正如你在上面的图片中所看到的，许多页面都有一些不变的元素或者变化很小的元素，比如页眉、页脚和其他框元素。如果你有一个像脸书这样的社交媒体应用程序，你甚至可能会有更多这样的应用程序，它的主体不会改变太多，但你会随着用户的互动不断添加更多的元素。

因此，每次从服务器请求一个新的资源，在每次请求中都得到相同的 HTML 标记，这是在浪费时间和空间。从用户的角度来看，这个问题是显而易见的。但是这也是开发者的一个问题。他们必须在每个页面上编写相同的 HTML 元素。除了复制粘贴之外，没有简单的方法来模块化和重用他们的代码。

**4。使用普通的 JavaScript 编辑 DOM(添加元素、更改属性等等)很难。这是非常多余和恼人的。这不会直接影响用户，但会使开发人员无法有效地调试和共享代码。**

那么，如果我们可以通过创建一个流畅的用户体验，以及一个更好的开发者体验来解决所有的问题呢？这就是框架允许我们做的。

每次发送请求时，我们不是发送一个页面，而是将整个 web 应用程序一次性发送给用户。这是一个很大的 JavaScript 文件，所以与单个页面相比，它可能会有点慢。但是之后，你就不用再联系服务器获取任何资源了，因为一切都在用户的电脑上。

这里的想法是当用户交互时，JavaScript 将决定向用户呈现什么；不会向服务器发送获取更多文件的请求。程序可能会发送一个请求来获取 JSON 格式的数据，但不是 HTML 和 CSS 文件。从用户的角度来看，这提供了一个本地的类似计算机的应用程序，在第一次加载后没有延迟地做他们想做的事情。

从程序员的角度来看，他们现在可以编写更少重复的模块化代码，因为他们不必重写多个 HTML 页面。他们只需编写一个大的 JavaScript 并重用不同页面上可能重复的元素。他们还可以通过使用框架工具轻松操作 DOM 来模拟呈现新页面的想法。

他们不必考虑更新 DOM 的繁琐步骤。此外，由于代码库更加简洁和模块化，他们现在可以轻松地测试、调试和与同事分享他们的工作。

简而言之，这就是 web 框架如何解决我们的一些问题。去享受学一个吧。一旦你知道你为什么学习它，你会发现它很有趣。你会发现这些框架是如何解决提到的问题的。

希望这有帮助！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)